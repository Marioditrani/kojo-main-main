<script >
  import {state} from '../state.js';
  import axios from 'axios'
  import sh from '../components/SHeader.vue'

  export default {
    components:{sh},

    data(){
        return{     
            state,
            arrProduct:[],
            arrCategory:[],
            categoryId: 0,
            name:'',
            phone:'',
            time:'',
            catinput:0,
            cartinput:0,
        }
    },
    methods:{
      cartopen(){
        if (this.cartinput){
          this.cartinput = 0
        }else{
          this.cartinput = 1
        }
        console.log(this.cartinput)
      },
      catopen(){
        if (this.catinput){
          this.catinput = 0
        }else{
          this.catinput = 1
        }
        console.log(this.catinput)
      },
      getProduct(cat){
        this.categoryId = cat,
        axios
				.get(state.baseUrl + 'api/projects', {
					params: {
						category: this.categoryId,
					},
				})
				.then(response => {
					this.arrProduct = response.data.results.data;
				});
      },
      getCategory(){
        axios
        .get(state.baseUrl + 'api/categories', {})
        .then(response => {
          this.arrCategory = response.data.results;
        });

      },
      changeCategory(value){
        if(value==1){
          this.getProduct(0)
          this.actvcat=value
          
        }else{
          this.getProduct(value)
          this.actvcat=value

        }
      },
      fixtag(arr){
        let arrtag='';
        arr.forEach((element, i) => {
          
          if(i+1==arr.length){
            
            arrtag = arrtag + element.name + '.'
          }else{
            arrtag = arrtag + element.name + ', '
            
          }
        });
        return arrtag
      },
      getPrice(cent){
        let num = parseFloat(cent);
        num = num / 100;
        num = "€" + num  

        return num
      },
      opencart(){
        if(state.sideCartValue){
          state.sideCartValue=0
        }else{
          state.sideCartValue=1
        }
      },
      sendOrder(){
        let data = {
          name:this.name,
          phone:this.phone,
          time:this.time,
          arrId:this.state.arrId,
          arrQt:this.state.arrQt,
          
        };
        axios.post(state.baseUrl + 'api/orders', {data}).then(response=>(response))
      },
      newItem(title, counter, tprice, price) {
        let newitem={
          title,
          counter,
          totprice: tprice,
          price: parseInt(price),
        }
        return newitem;
      },
      addItem(title, counter, price, id){
        if(counter<=0){
          return console.log('ci hai provato amico!')
        }
        let check= false;
        let newitem= this.newItem(title, counter, price*counter, price);
        console.log(newitem);
        this.state.arrCart.forEach((element, index) => {
          if(element.title == title){
            element.counter += counter
            element.totprice = element.counter * element.price
            check=true
            this.state.arrQt[index] += counter
          }

        });
      
        if(!check){
          this.state.arrCart.push(newitem);
          this.state.arrId.push(id)
          this.state.arrQt.push(counter)
        }
        this.arrProduct.forEach(element => {
          if(element.name == title){
            element.counter = 0
          }
        });
        this.getTot();
      },
      removeItem(title){
        this.state.arrCart.forEach((element, i) => {
          if(element.title== title){
            if(element.counter>=0){
            element.counter --;
            element.totprice -= element.price
            this.state.arrQt[i]--;
            }if(element.counter == 0){
              let nwi = i - 1;
              this.state.arrId.splice(i, 1)
              this.state.arrQt.splice(i, 1)
              let newarrCart = this.state.arrCart.filter((element) => {
                return element.title !== title;
              });
              this.state.arrCart=[];
              this.state.arrCart = newarrCart;
              }
          }
        });

        this.getTot();

      },
      upCounter(id){
        this.arrProduct.forEach(element => {
          if(element.id == id){
            element.counter ++
          }
        });

      },
      downCounter(id){
        this.arrProduct.forEach(element => {
          if(element.id == id){
            if(element.counter>=1){
              element.counter --
            }
          }
        });
      },
      getTot(){
        this.state.totCart = 0
        this.state.arrCart.forEach(element => {
          console.log(element.totprice)
          this.state.totCart = this.state.totCart + element.totprice
        });
      }
    },
    created(){
      this.getProduct(0);
      this.getCategory();

     
      this.state.actvPage = 5;
    },

  }
</script>
<!-- :class="state.sideCartValue ?  'sub-item-off' : 'sub-item-on tag'" -->
<template>
  <div class="prenota">
   <sh class="sh"/>
    
    <div class="prenota-cont">
      <div class="top-respo">
        <h1>Prenota il tuo Asporto</h1>
        <img src="../assets/img/crop.png" alt="" class="bacchette-respo">
      </div>
      <img src="../assets/img/crop.png" alt="" class="bacchette">
      <div class="top-prenota">
        <div class="left-top">
          <h1>Prenota il tuo Asporto</h1>
        </div>
        <div class="right-top">
          <div class="one-category" @click="catopen(catinput)" :class="catinput ?  'cat-off': 'cat-on'">
              <span>categorie</span>
            </div>
          <div class="categorie"   :class="catinput ? 'cat-on': 'cat-off'">
            <div v-for="cat in arrCategory" :key="cat.id" class="category" :class="actvcat == cat.id ? 'category-on' : '' " @click="changeCategory(cat.id)"> 
              <span @click="catopen(catinput)" :class="actvcat == cat.id ? 'span-on' : '' ">{{ cat.name }}</span>
            </div>
          </div>
          <div class="cart-close" @click="cartopen(cartinput)" :class="cartinput ?  'cat-off': 'cat-on'">
            <div class="img-cart">
              <svg   xmlns="http://www.w3.org/2000/svg" width="30" height="30" fill="currentColor" class="bi bi-cart-fill" viewBox="0 0 16 16"> <path d="M0 1.5A.5.5 0 0 1 .5 1H2a.5.5 0 0 1 .485.379L2.89 3H14.5a.5.5 0 0 1 .491.592l-1.5 8A.5.5 0 0 1 13 12H4a.5.5 0 0 1-.491-.408L2.01 3.607 1.61 2H.5a.5.5 0 0 1-.5-.5zM5 12a2 2 0 1 0 0 4 2 2 0 0 0 0-4zm7 0a2 2 0 1 0 0 4 2 2 0 0 0 0-4zm-7 1a1 1 0 1 1 0 2 1 1 0 0 1 0-2zm7 0a1 1 0 1 1 0 2 1 1 0 0 1 0-2z"/> </svg>
            </div>
            
          </div>
          <div class="cart" :class="cartinput ?  'cat-on': 'cat-off'">
            <div class="img-cartclose">
              <svg xmlns="http://www.w3.org/2000/svg"  @click="cartopen(cartinput)" :class="cartinput ?  'cat-on': 'cat-off'"    width="30" height="30" fill="currentColor" class="bi bi-cart-x-fill" viewBox="0 0 16 16"><path d="M.5 1a.5.5 0 0 0 0 1h1.11l.401 1.607 1.498 7.985A.5.5 0 0 0 4 12h1a2 2 0 1 0 0 4 2 2 0 0 0 0-4h7a2 2 0 1 0 0 4 2 2 0 0 0 0-4h1a.5.5 0 0 0 .491-.408l1.5-8A.5.5 0 0 0 14.5 3H2.89l-.405-1.621A.5.5 0 0 0 2 1H.5zM6 14a1 1 0 1 1-2 0 1 1 0 0 1 2 0zm7 0a1 1 0 1 1-2 0 1 1 0 0 1 2 0zM7.354 5.646 8.5 6.793l1.146-1.147a.5.5 0 0 1 .708.708L9.207 7.5l1.147 1.146a.5.5 0 0 1-.708.708L8.5 8.207 7.354 9.354a.5.5 0 1 1-.708-.708L7.793 7.5 6.646 6.354a.5.5 0 1 1 .708-.708z"/></svg>

            </div>
            <div :class="state.sideCartValue ? 'content-cart' : 'ccoff'" >
              <div class="span" v-if="!state.arrCart.length && !state.sideCartValue">Il carrello è vuoto</div>
              <div v-for="item in state.arrCart" :class="state.sideCartValue ?  'item-off' : 'item-on'" :key="item.id">
                <div>{{ item.title }}</div>
                <div>{{ getPrice(item.totprice) }}</div>
                <div>x {{ item.counter }}</div>
                <svg :class="state.sideCartValue ?  'sub-item-off' : 'sub-item-on'" @click="removeItem(item.title)"  style="color: white" xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="current-color" class="bi bi-trash" viewBox="0 0 16 16"> <path d="M5.5 5.5A.5.5 0 0 1 6 6v6a.5.5 0 0 1-1 0V6a.5.5 0 0 1 .5-.5zm2.5 0a.5.5 0 0 1 .5.5v6a.5.5 0 0 1-1 0V6a.5.5 0 0 1 .5-.5zm3 .5a.5.5 0 0 0-1 0v6a.5.5 0 0 0 1 0V6z" fill="white"></path> <path fill-rule="evenodd" d="M14.5 3a1 1 0 0 1-1 1H13v9a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V4h-.5a1 1 0 0 1-1-1V2a1 1 0 0 1 1-1H6a1 1 0 0 1 1-1h2a1 1 0 0 1 1 1h3.5a1 1 0 0 1 1 1v1zM4.118 4 4 4.059V13a1 1 0 0 0 1 1h6a1 1 0 0 0 1-1V4.059L11.882 4H4.118zM2.5 3V2h11v1h-11z" fill="white"></path> </svg>
              </div>
              <div class="bottom-cart">
                <router-link :to="{ name: 'conferma' }" v-if="state.arrCart.length && !state.sideCartValue" class="next">Completa ordine</router-link>
                <div class="tot">
                  <span>TOTALE</span>
                    {{ getPrice(state.totCart)}}
                  
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
      
      <div class="main-prenota">

        <div class="card-wrap"  v-for="item in arrProduct" :key="item.id">
          <div class="card">
            <div class="title">{{ item.name }}</div>
          <img src="../assets/img/imgsushi.png" alt="">
          <div class="c-tp">
            <div class="tags"> <span>{{fixtag(item.tags) }}</span></div>
            <div class="price">{{ getPrice(item.price) }}</div>
          </div>
          <div class="add">
            <div class="sec">
              <span class="minus"  @click="downCounter(item.id)">-</span>
              <span class="counter">{{ item.counter }}</span>
              <span class="plus" @click="upCounter(item.id)" >+</span>
            </div>
          <div class="mybtn" @click="addItem(item.name, item.counter, item.price, item.id)">aggiungi</div>
          </div>
        </div>
        </div>
      
  
      </div>
    </div>
    
  </div>
</template>

<style scoped lang="scss">
@use '../assets/styles/general.scss' as *;



.prenota-cont::-webkit-scrollbar{
      
      width: 10px;
      height: 10px;
      
  }

.prenota-cont::-webkit-scrollbar-thumb {
    border-radius: 20px;
    background: $c-header;
    
}
.prenota-cont::-webkit-scrollbar-track {
    border-radius: 20px;
    background: rgba(52, 4, 7, 0.786);
    
}
.prenota-cont::-webkit-scrollbar-thumb:hover {
    border-radius: 20px;
    background-color: $c-nav-link;
    border: 2px solid $c-header;
    
}
.hd{box-shadow: 10px 10px 10px black; }

.sh{
  position: absolute;
  top: 0;
  right: 0;
}
.prenota{
  overflow: hidden;
  display: flex;
  flex-direction: column;
  position: fixed;
  bottom: 0;
  left: 0;
  width: 100vw;

  .prenota-cont{
    width: 100vw;
    background-color: #270000;
    overflow: auto;
    height: 100%;
    padding: 1rem 1rem ;

    .top-respo{
      display: none;
    }
    h1{
      text-align: center;
      text-transform: uppercase;
      padding: 1rem;
      font-size: 50px;
    }

    .bacchette{
      position: fixed;
      left: 0;
      bottom: 2;
    }
    
    .top-prenota{
      display: flex;
      justify-content: space-between;
      width: 70%;
      margin: auto;
    }
    
    .main-prenota{
      margin-top: 7rem;
      @include dfc;
      flex-wrap: wrap;
      gap: 3rem;
      align-items: stretch;
      .card-wrap{
        width: calc((75% - 2rem) / 3);
        margin-bottom: 60px;
        @include dfc;
        align-items: stretch;
        .add{
          position: absolute;
          //background-color: red;
          bottom: -50px;
          left: 0;
          width: 100%;
          @include dfc;
          gap: 2rem;
            .sec{
              @include dfc;
              gap: .5rem;

              .plus, .minus{
                height: 3rem;
                width: 3rem;
                @include dfc;
                border: 2px solid white;
                border-radius: 50px;
                font-size: 25px;
              }
            }
            .mybtn{
              padding: .5rem 2rem;
              text-transform: uppercase;
              border: 2px solid white;
              border-radius: 20px;
              font-size: 25px;
            }
            
          }

        .card{
        width: 100%;
        border-radius: 10px;
        padding: 20px;
        position: relative;
        display: flex;
        flex-direction: column;
        justify-content: center;
        margin: 4rem 1rem;
        margin-bottom: 130px;
          
          img{
          position: absolute;
          top: -160px;
          left: 0;
          right: 0;
          margin: auto;
          width: 300px;
          
          }
          .title{
          font-size: 20px;
          width: 100% ;
          text-transform: upercase;
          position: absolute;
          left:45px;
          top:20px;
          z-index: 10001;
          padding: .5rem;
          }
          .c-tp{
          background-color: #AB2F2F;
          position: relative;
          z-index: 10000;
          width: 100%;
          height: 100%;
          display: flex;
          flex-direction: column;
          padding: 2rem;
          border-radius: 20px;
          justify-content: space-between;
          
            
            .tags, .price{
              border-radius: 10px;
            width: 100%;
            padding-right: .5rem;
            padding-bottom: .5rem;
            }
            .tags{
  
              display: flex;
            padding-top: 1rem;
            padding-right: .5rem;
            span{
              font-size: 13px;
              font-family:'Lucida Sans', 'Lucida Sans Regular', 'Lucida Grande', 'Lucida Sans Unicode', Geneva, Verdana, sans-serif;
              font-weight: bold!important; 

  
              }
            }
            .price{
              width: 100%;
              //border-radius: 10px ;
              text-align: right;
    
            }
          }
        }

      }

    }
    
  }


}

/*** */

.right-top{
  display: flex;
  flex-direction: column;
  align-items: flex-end;
}
.one-category{
  background-color: #523333;
  width: 350px;
  height: 80px;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 4px;
  
  margin: 0 auto;
  z-index: 10;
  position: relative;
  border: 5px solid white;
  border-radius: 50px;
  margin: 40px 0;
  span{
    font-size: 30px;
    
    text-align: center;
    transition: all .5s;
    text-transform: uppercase;
    
    letter-spacing: .1em;
  }
}
.categorie {
  box-shadow: -40px 50px 100px black ;
  background-color: #523333;
  max-width: 600px;
  width: 90%;
  height: 300px;
  border-radius: 4px;
  display: flex;
  flex-direction: column;
  gap: 5px;
  padding: 1.5em 1em;
  margin: 0 auto;
  z-index: 10;
  position: relative;
  border: 5px solid white;
  border-radius: 20px;
  .category {
   height: 100%;
   flex: 1;
   overflow: hidden;
   cursor:grab;
   border-radius: 2px;
   transition: all .5s;
   background-color: $c-footer-nav ;
   border: 1px solid $c-nav-link;
   display: flex;
   
   justify-content: center;
   align-items: center;
   span {
    min-width: 30em;
    padding: .5em;
    text-align: center;
    transition: all .5s;
    text-transform: uppercase;
    color: $c-nav-link;
    letter-spacing: .1em;
   }
  }
  .category:hover {
    
  }
  .category:hover span {
    color: white;
   transform: rotate(0);
  }
}

.category-on {
  
  background-color: $c-header !important;
}
.category-on:hover {
  
  background-color: $c-header !important;
}
.span-on{
  color: white!important;;

}

.cat-off{display: none;}
/***** */

.cart-close{
  display: none;
  display: flex;
  justify-content: flex-end;
  padding: 1rem 0;
  
  .img-cart{
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: #523333;
    width: 70px;
    height: 70px;
    border: 3px solid white;
    border-radius: 50px;
  }
}

.cart{
  display: flex;
  flex-direction: column;
  position: relative;
  box-shadow: -40px 50px 100px black ;
  .img-cartclose{
    display: flex;
    justify-content: center;
    align-items: center;
    position: absolute;
    right: -2px;
    top: -7px;
    width: 70px;
    height: 70px;
    background-color: #523333;
    border: 3px solid white;
    border-radius: 50px;
    
  }

  color: $c-nav-link;
  border: 3px solid white;
  background-color: #523333;
  max-width: 450px;
  width: 100%;
  border-radius: 50px;
  padding: .4rem;
  margin: 0 auto;
  .top-cart{
    padding: .2rem;
    @include dfc;
    justify-content: space-between;
  }

  .bottom-cart{
    display: flex;
    gap: 2rem;

    .tot{
      display: flex;
      flex-direction: column;
    }
  }
}
.next{
    border: 3px solid white;
    text-transform: uppercase;
    padding: 10px ;
    text-align: center;
    border-radius: 20px;
  }
.content-cart{
  width: 10px;
  height: 0;
  padding: 0rem;
  display: flex;
  flex-direction: column;
  transition: all .2s linear ;
}
.ccoff{
  padding: 2rem;
  padding-top: 4rem;
  height: 100%;
  display: block;
  display: flex;
  flex-direction: column;
  gap: 1rem;
  transition: all .2s linear ;
  
  
}
.item-off{
  opacity: 0;
  display: flex;
  justify-content: space-between;
  transition: all .2s linear .2s;
  
}
.item-on{
  display: flex;
  justify-content: space-between;
  height: auto;
  opacity: 1;
  transition: all .2s linear .2s;
  div{
    width: 45%;
  }
  svg{
    width: 10%;
  }
  
}

.cat-off{display: none;}

@media (max-width:$bp2) {
  .card-wrap{
    width: 95% !important;
  }
  .add{
        flex-direction: row;
  }
}
@media (max-width:$bp1) {
  .menu{
    width:100%;
  }
  
}
@media (max-width:1600px) {
  .add{
    flex-direction: column;
    gap: 1rem!important;
    bottom: -110px!important;
    left: 0;
  }

  .card-wrap{
    width: calc((75% - 2rem) / 2)!important;
  }
  
}

@media (max-width:1100px) {
  .add{
    flex-direction: column;
    gap: 1rem!important;
    bottom: -110px!important;
    left: 0;
  }

  .card-wrap{
    width: 95%!important;
  }
  
  .bacchette{
    display: none!important;
  }
  .left-top{
    h1{
      display: none;
    }
  }

  .top-respo{
    width: 70%;
    display: flex!important;
    flex-direction: row-reverse;
    justify-content: space-between;
    margin: auto;
    h1{
      text-align: end!important;
      width: 50%;
    }
    

    .bacchette-respo{
      width: 90px!important;
      transform: rotateZ(120deg);
    }
  }
  .top-prenota{
    justify-content: center!important;
  }
  .right-top{
    align-items: center!important;
  }
}

@media (max-width:700px) {
  .card-wrap{
    width: 95%!important;
  }
  h1{
    font-size: 40px!important;
    width: 40%!important;
  }
 .bacchette-respo{
  width: 50px!important;
      
  }


  

}
</style>
