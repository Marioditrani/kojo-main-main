<script >
  import {state} from '../state.js'


  export default {
    components:{},

    data(){
        return{     
            state,
        }
    },
    created(){
   
      this.state.actvPage = 3;
    }
    
  }
</script>

<template>
 <div class="bg-chisiamo">

   <div class="about">
     <img src="../assets/img/crop.png" alt="" class="bacchette">
     <div class="main-about">
       <div class="top-about">
         <img src="../assets/img/cuoco-sushi1.png" alt="" class="cuoco1">
         <h1>Chi  siamo?</h1>
       </div>
       <div class="post-container">
         <div class="post">
           
           <div class="text">
             <h4>IL NOSTRO MODO DI CUCINARE</h4>
             <p>
               Esplorate le radici profonde della cucina cinese attraverso piatti come il "Jiaozi", ravioli tradizionali cinesi, riempiti di sapori autentici che risalgono a generazioni. Dall'agrodolce.
             </p>
           </div>
           <img src="../assets/img/cuochi-sushi-21.png" alt="">
         </div>
         <div class="post">
           
           <div class="text">
             <h4>IL NOSTRO MODO DI CUCINARE</h4>
             <p>
               Esplorate le radici profonde della cucina cinese attraverso piatti come il "Jiaozi", ravioli tradizionali cinesi, riempiti di sapori autentici che risalgono a generazioni. Dall'agrodolce.
             </p>
           </div>
           <img src="../assets/img/cuochi-sushi-21.png" alt="">
         </div>
         
         
       </div>
       
     </div>
    </div>
 </div>

   


</template>

<style scoped lang="scss">
@use '../assets/styles/general.scss' as *;

@media (max-width:$bp1) {.btn-menu{display:block;}}
.about::-webkit-scrollbar{
  width: 10px;
}
.about::-webkit-scrollbar-thumb {
  border-radius: 20px;
  background: $c-header;
}
.about::-webkit-scrollbar-thumb:hover {
  border-radius: 20px;
  background-color: $c-nav-link;
  border: 2px solid $c-header;
    
}

.bg-chisiamo{
  height: 100%;
  margin-top: 230px;
  width: 100%;
}
.about{
  background-color: #270000;
  overflow: hidden;
  display: flex;
  flex-direction:column;
  width: 100%;
  height: 100%;
  margin-top: 230px;
  position: fixed;
  overflow: auto;
  top: 0;
  padding-bottom: 250px;
  .bacchette{
    max-width: 200px;
    position: fixed;
    bottom: 150px;
    left: -30px!important; 
    transform: scaleX(-1); 
  }
  .main-about{
    margin:auto;
    width: 70%;
    
    padding: 2rem;
   
   
    .top-about{
      display: flex;
      h1{
        font-size: 100px;
        width: 100%;
        text-align: center;
      }
      .cuoco1{
        position: relative;
          z-index: 1;
      }
    }
    .post-container{
      margin-top: 2rem;
      display: flex;
      flex-direction: column;
      gap: 2rem;
      .post::after{
        content: ' ';
        display: block;
        background-color: rgba(16, 16, 16, 0.832);
        position: absolute;
        height: 100%;
        width: 100%;
        top: 0;
        bottom: 0;
        left: 0;
        right: 0;
        z-index: 2;
    
      }
      .post:nth-child(even){
        flex-direction: row-reverse;
      }
      
      
      .post{
        @include dfc;
        flex-direction: reverse;
        z-index: 1;
        gap: 8rem;
        padding: 2rem;
        background-position: top;
        background-size: cover;
        position: relative;
        .text{
          text-align: center;
          position: relative;
          z-index: 3;
          display: flex;
          flex-direction: column;
          gap: 5rem;
          width: 40%;
          h4{
            font-size: 22px;
            
          }
          p{
            font-size: 20px;
          }
        }
        img{
          position: relative;
          z-index: 3;
          width: 43%;
          max-width: 400px;
          box-shadow: 17px 10px 38px black;
        }
      }
    }
  }
}


@media (max-width:$bp3){
  .post{
    display: flex;
    flex-direction: column !important;
    img{
      width: 70% !important;
    }
    .text{
      width: 70% !important;
    }
  }
}
@media (max-width: 1300px){
  .about{
    margin-top:150px!important;
  }
}
@media (max-width:1100px){
  .main-about{
    width: 90%!important;
    
  }
  .bacchette{
    max-width: 150px!important;
    left: -80px!important;
  }
}
@media (max-width:850px){
  .bacchette{
    display: none;
  }
  .about{

    .main-about{
  
      .top-about{
        .cuoco1{
          width: 200px!important;
        
        }
        h1{
          font-size: 70px;
        }
      }
    }
  }
}
@media (max-width:550px){

  .about{

    .main-about{
      .post:after{
        padding: 1rem!important;
      }
      .top-about{
        h1{
          font-size: 60px;
        }
      }
    }
  }
}
@media (max-width:530px){

.about{

  .main-about{
    .post:after{
        padding: 0rem!important;
      }
    .top-about{
      .cuoco1{
        width: 170px!important;
      }
      h1{
        font-size: 50px;
      }
    }
  }
}
}
@media (max-width:430px){
.bacchette{
  display: none;
}
.about{

  .main-about{
    
    .top-about{
      flex-direction: column-reverse;
      align-items: center;
      gap: 1rem;
      .cuoco1{
        
        
      }
      h1{
        font-size: 50px;
      }
    }
  }
}
}



</style>