
<script >
  import {state} from '../state.js';
  

 export default{
  data(){
    return{
      state,
      infomenu: 0,
    }
  },
  methods: {
    infoside() {
        if (this.infomenu) {
            this.infomenu = 0
        } else {
            this.infomenu = 1
        }
        },
    }
 }
</script>


<template>
  <div class="nav">
    <div class="left-nav">
      <img src="../assets/img/logo_kojo.jpg" alt="">
    </div>
    <div class="right-nav">
      <div class="nav1">
        <img src="../assets/img/punta1.png" alt="">
        <div class="right-nav1"></div>
      </div>
      <div class="nav2">
        <img src="../assets/img/punta2.png" alt="">
        <div class="menu">
          <router-link :to="{ name: 'home' }" :class="state.actvPage == 1 ? 'active-link' : '' " class="nav-link" @click="state.updateActvPage(1)" >home</router-link>
          <router-link :to="{ name: 'menu' }" :class="state.actvPage == 2 ? 'active-link' : '' " class="nav-link" @click="state.updateActvPage(2)" >menu</router-link>
          <router-link :to="{ name: 'prenota' }" :class="state.actvPage == 5 ? 'active-link' : '' " class="nav-link" @click="state.updateActvPage(5)" >Ordina d'Asporto</router-link>
          <router-link :to="{ name: 'prenotaServizio' }" :class="state.actvPage == 6 ? 'active-link' : '' " class="nav-link" @click="state.updateActvPage(6)" >Prenota tavolo</router-link>
        </div>

      </div>
      <div class="nav3">
        <img src="../assets/img/punta3.png" alt="">
        <div class="right-nav3"></div>
      </div>
      <div class="nav4">
        <div class="left-nav4">
          <img src="../assets/img/puntacsleft.png" alt="">
          <div class="chi-siamo"><router-link :to="{ name: 'chi-siamo' }" :class="state.infomenu ? 'menu-off': 'active-link' " class="nav-link" @click="state.updateActvPage(3)" >chi siamo?</router-link></div>
          <img src="../assets/img/puntacsright.png" alt="">
        </div>
        <div class="center-nav4">

        </div>
        <div class="right-nav4">
          <img src="../assets/img/puntac.png" alt="">
          <div class="contatti"><router-link :to="{ name: 'contatti' }" :class="state.infomenu ? 'menu-off': 'active-link' " class="nav-link" @click="state.updateActvPage(4)" >contatti</router-link></div>
        </div>
      </div>
    </div>
    <div class="nav-mb">
      <div class="t-mb"></div>
      <div class="btn-menu" @click="state.openside" :class="state.sideMenuValue? 'btn-off' : 'btn-on'">
        <div class="l1"></div>
        <div class="l2"></div>
        <div class="l1"></div>
      </div>
    </div>
  </div>
  
  

  <div class="nav-mb">
    <div :class="state.sideMenuValue ? 'burger-close-on' : 'burger-close-off'" @click="state.openside">
      <div class="line"  :class="state.infomenu ?   'menu-off': 'active-link' "></div>
      <div class="line l1" :class="state.infomenu ?   'menu-off': 'active-link' "></div>
    </div>
    <div :class="state.sideMenuValue ? 'top-on' : 'top-off'">
      <div class="top-menu" :class="state.infomenu ? 'top-off' : 'top-on'">
        <router-link :to="{ name: 'home' }" :class="state.infomenu ?   'menu-off': 'active-link' " class="nav-link" @click="state.updateActvPage(1)" >home</router-link>
        <router-link :to="{ name: 'menu' }" :class="state.infomenu ? 'menu-off': 'active-link' " class="nav-link" @click="state.updateActvPage(2)" >menu</router-link>
        <router-link :to="{ name: 'chi-siamo' }" :class="state.infomenu ? 'menu-off': 'active-link' " class="nav-link" @click="state.updateActvPage(3)" >chi siamo?</router-link>
        <router-link :to="{ name: 'contatti' }" :class="state.infomenu ? 'menu-off': 'active-link' " class="nav-link" @click="state.updateActvPage(4)" >contatti</router-link>
        <router-link :to="{ name: 'prenota' }" :class="state.infomenu ? 'menu-off': 'active-link' " class="nav-link" @click="state.updateActvPage(5)" >Ordina d'Asporto</router-link>
        <router-link :to="{ name: 'prenotaServizio' }" :class="state.infomenu ? 'menu-off': 'active-link' " class="nav-link" @click="state.updateActvPage(6)" >Prenota tavolo</router-link>
      </div>
      <div class="nav-link info" @click="state.infoside" :class="state.infomenu ? 'infoopen' : 'infoclose'">
        <div class="top-info">
          <div class="info-n" :class="state.infomenu ? 'info-on' : 'info-n'">info</div>
          <div class="info-n" @click="state.infoside" :class="state.infomenu ? 'info-btn' : 'info-n'">+</div>
        </div>
        <div class="infosideopen" :class="state.infomenu ? 'infosideopen' : 'infosideclose'">
          <div class="topinfo" :class="state.infomenu ? '' : 'topinfoclose'">
            <div class="sec-1">
              <h4>Dove puoi trovarci</h4>
              
            </div>
            <div class="sec-2">
                <h4>Orari d'apertura</h4>
                <div class="cont-giorni">
                  <span>lunedì</span>
                  <span>martedì</span>
                  <span>giovedì</span>
                  <span>venerdì</span>
                  <span>sabato</span>
                  <span>domenica</span>
              </div>
              <div class="cont-orari">
                <span class="time" >chiusi</span>         
                <span class="time" >16:00 - 22:00</span>
                <span class="time" >16:00 - 22:00</span>
                <span class="time" >16:00 - 22:00</span>
                <span class="time" >16:00 - 22:00</span>
                <span class="time" >16:00 - 22:00</span>
              </div>
            </div>
            <div class="sec-3">
               PI: 1231231231231, privacy policy, product by FUTURE+
            </div>
          </div>
        </div>
      </div>
      
    </div>
    
  </div>
</template>


<style lang="scss" scoped>
@use '../assets/styles/general.scss' as *;

.info-n{
  position: relative;
  z-index: 300;
}
.nav-link.info{
  display: flex;
  flex-direction: column;
  gap: 10px;

  .top-info{
    width:100%;
    display:flex;
    justify-content: space-between;
  }
}

.infoopen{
height:100%;
background-color:$c-footer-nav;
width:100%;
justify-content: space-between;
transition: all 1s linear;
}
.infoclose{
height: 0%;
}

.info-on{
  padding:20px;
  font-size:40px;
}
.info-btn{
  transform: rotateZ(45deg);
  font-size:40px;
  padding:20px;
}

.infosideopen{
  height: auto;
  text-align:center;
  .sec-1{
      @include dfj;
      flex-direction: column;
      gap: 1rem;
      width: 100%;
      padding-bottom: 100px;

      h4{
        font-size:30px;
        padding-bottom:10px;
      }
      p{
        font-size:25px;
      }
    }
    .sec-2{
      @include dfj;
      flex-wrap: wrap;
      gap: 1rem;
      width: 100%;
      justify-content: space-around;
      h4{
        
        width: 100%;
        padding-bottom:30px;
        font-size: 30px;
      }
      .cont-giorni, .cont-orari{
        font-size: 15px;
        @include dfj;
        flex-direction: column;
        gap: .5rem;
        text-align: left;
        text-transform: uppercase;
        
        .time{
          text-align: center;
        }
      }
      padding-bottom: 50px;
    }
    .sec-3{
      background-color: rgba(0, 0, 0, 0.43);
      font-size: 10px;
      padding: 10px;
    }
    
}
.topinfoclose{
  display:none;
}
.nav{
  background-color: white;
  display: flex;
  width: 100%;
  height: 230px;
  position: fixed;
  top: 0;
  left: 0;
  z-index: 100;
  .left-nav{
    padding-left: 150px;
    height: 100%;
    @include dfc;
    img{
      height: 80%;
    }
  }
  .right-nav{
    align-items: flex-end;
    display: flex;
    height: 100%;
    flex-direction: column;
    width: 100%;
    
    .nav1{
      display: flex;
      height: 56px;
      width: 90%;
      margin-bottom: 8px;
      img{
        height: 100%;
      }
      .right-nav1{
        background-color: #523333;
        width: 100%;
      }
      
    }
    .nav2{
      margin-bottom: 8px;
      display: flex;
      height: 48px;
      width: 85%;
      img{
        height: 100%;
      }
      .menu{
        background-color: #712A2A;
        width: 100%;
        display: flex;
        justify-content: space-between;
        align-items: center;
        padding: 0 200px 0 100px;
        font-size: 20px;
        text-transform: uppercase;
      }
    }
    .nav3{
      display: flex;
      height: 40px;
      width: 86%;
      img{
        height: 100%;
      }
      .right-nav3{
        background-color: #523333;
        width: 100%;

      }
    }
    .nav4{
      text-transform: uppercase;
      display: flex;
      height: 70px;
      width: 85%;
      img{
        height: 100%;
      }
      
      .left-nav4{
        display: flex;
        .chi-siamo{
          @include dfc;
          font-size: 20px;
          color: white;
          background-color: #270000;
          border-top: 8px solid white;          
          border-bottom: 8px solid white;          
          width: 200px;
        }
      }

      .center-nav4{
        background-color: #523333;
        width: 100%;
        height: 100%;
      }
      .right-nav4{
        display: flex;
        img{
          height: 100%;
        }
        .contatti{
          @include dfc;
          font-size: 20px;
          color: white;
          background-color: #270000;
          border-top: 8px solid white;          
          border-bottom: 8px solid white;         
          border-right: 8px solid white; 
          width: 200px;
        }
      }
    
    }
  }

  .nav-mb{
    display: none;
    position: relative;
    z-index: 5315;
    background-color: #523333;
    width: 100%;
    height: 140px;

    .t-mb{
    width: 30%;
    height: 140px;
    background-color: #523333;
    width: 25%;
    border-left: 0px solid transparent;
    border-right: 90px solid transparent;
    border-bottom: 140px solid white;
    -moz-transform:rotate(0);
    -webkit-transform:rotate(0);
    -ms-transform:rotate(0);
    -o-transform:rotate(0);
    transform:rotate(0);
    position: relative;
    z-index: 0;

    
  }
  .btn-menu{
    position: fixed;
    right: 50px;
    top: 50px;
    z-index: 20;
    flex-direction: column;
    gap: .7rem;
    align-items: flex-end;
    display: flex;
    .l1{
      width: 40px;
      height: 5px;
      border-radius: 20px;
      background-color: white;
      
    }
    .l2{
      width: 50px;
      height: 5px;
      border-radius: 20px;
      background-color: white;
     
    }
    
    
  }
    
    
  }
}
.nav-mb-on{
  position: fixed;
  top: 0;
  right: 0;
  z-index: 10;
  background-color: #270000;
  width: 100%;
  height: 100%;
  transition: all .3s linear;
}
.burger-close-on{
  transition: all 1s linear 2s;
  position: fixed;
  top: 8%;
  right: 8%;
  opacity: 1;
  transition: display .3s linear;
  transition: opacity 1s linear 2s;
  z-index: 201;
  .line{
    background-color: white;
    height: 30px;
    width: 5px;
    transform: rotateZ(45deg);
    position: absolute;
    transition: display .3s linear;
  transition: opacity 1s linear 2s;
  }
  .l1{
    transform: rotateZ(135deg)
  }
}
.top-on{
  @include dfc;
  height: 100vh;
  justify-content: space-around;
  flex-direction: column;
  padding: 10%;
  opacity: 1 ;
  transition: display .3s linear 1s!important;
  transition: opacity 5s linear 2s;
  background-color: #270000;
  position: relative;
  z-index: 200;
  .nav-link{
    text-transform: uppercase;
    line-height: 1rem;
    color: white;
    font-family: 'Gabarito', cursive;
    font-size: 1.8rem;
  }

}

.bottom-footer-on{
  display: none;
}
.nav-mb-off{
  position: fixed;
  top: 0;
  left: 0;
  z-index: 10;
  background-color: $c-nav;
  width: 100%;
  height: 0;
  transition: all .2s linear;


}
.burger-close-off{

  display: none;
  opacity: 0;
  transition: display .3s linear;
  transition: opacity 1s linear 2s;
  
}
.top-off{
  display: none;
  opacity: 0;
  transition: display .3s linear;
  transition: opacity 1s linear 2s;
}
.bottom-footer-off{
  display: none;
}


@media (max-width: 1500px) {

  .nav{
    .nav1{
      width: 91%!important;
    }
    .nav3{
      width: 86%!important;
    }
    .nav4{
      width: 84.5%!important;
    }

  }
  .menu{
    padding: 0 100px 0 100px!important;
  }
}
@media (max-width: 1350px) {
  .menu{
    padding: 0 50px 0 50px!important;
  }
}
@media (max-width: 1300px) {
  .nav{
    height: 150px;
    .right-nav{
      display: none;
    }
  }
  .nav-mb{
    display: block!important;
  }
}

@media (max-width: 600px){
  .nav{
    .left-nav{
        padding-left:0px!important;
      
    }
  }
}
@media (max-width: 450px){
  .nav-mb{
   
    .btn-menu{
      right: 20px!important;
    }
  }
}
@media (max-width: 400px){
  
  .nav-mb{
   
    .btn-menu{
      right: 20px!important;
    }
  }
}

</style>


