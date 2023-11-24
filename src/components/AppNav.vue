
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
        <div class="menu"></div>
      </div>
      <div class="nav3">
        <img src="../assets/img/punta3.png" alt="">
        <div class="right-nav3"></div>
      </div>
      <div class="nav4">
        <div class="left-nav4">
          <img src="../assets/img/puntacsleft.png" alt="">
          <div class="chi-siamo">Chi siamo</div>
          <img src="../assets/img/puntacsright.png" alt="">
        </div>
        <div class="center-nav4">

        </div>
        <div class="right-nav4">
          <img src="../assets/img/puntac.png" alt="">
          <div class="contatti  ">Contatti</div>
        </div>
      </div>
    </div>
  </div>
  <!-- <div class="nav">
    <div class="left-nav">
      <div class="img">

        <img src="../assets/img/logo_kojo.jpg" alt="">
      </div>
    </div>
    <div class="t-mb"></div>
    <div class="right-nav">
      <div class="link">
        <router-link :to="{ name: 'home' }" :class="state.actvPage == 1 ? 'active-link' : '' " class="nav-link" @click="state.updateActvPage(1)" >home</router-link>
        <router-link :to="{ name: 'menu' }" :class="state.actvPage == 2 ? 'active-link' : '' " class="nav-link" @click="state.updateActvPage(2)" >menu</router-link>
        <router-link :to="{ name: 'prenota' }" :class="state.actvPage == 5 ? 'active-link' : '' " class="nav-link" @click="state.updateActvPage(5)" >Ordina d'Asporto</router-link>
        <router-link :to="{ name: 'prenotaServizio' }" :class="state.actvPage == 6 ? 'active-link' : '' " class="nav-link" @click="state.updateActvPage(6)" >Prenota tavolo</router-link>
        <router-link :to="{ name: 'chi-siamo' }" class="chi-siamo" ><p>Chi siamo?</p></router-link>
        <router-link :to="{ name: 'contatti' }" class="contatti" > <span>Contatti</span></router-link>
      </div>
      
      <div class="bg-mb">

      </div>
    </div>
  </div> -->

  <div :class="state.sideMenuValue ? 'nav-mb-on' : 'nav-mb-off'">
    <div :class="state.sideMenuValue ? 'burger-close-on' : 'burger-close-off'" @click="state.openside">
      <div class="line"  :class="state.infomenu ?   'menu-off': 'active-link' "></div>
      <div class="line l1" :class="state.infomenu ?   'menu-off': 'active-link' "></div>
    </div>
    <div :class="state.sideMenuValue ? 'top-on' : 'top-off'">
      <router-link :to="{ name: 'home' }" :class="state.infomenu ?   'menu-off': 'active-link' " class="nav-link" @click="state.updateActvPage(1)" >home</router-link>
      <router-link :to="{ name: 'menu' }" :class="state.infomenu ? 'menu-off': 'active-link' " class="nav-link" @click="state.updateActvPage(2)" >menu</router-link>
      <router-link :to="{ name: 'chi-siamo' }" :class="state.infomenu ? 'menu-off': 'active-link' " class="nav-link" @click="state.updateActvPage(3)" >chi siamo?</router-link>
      <router-link :to="{ name: 'contatti' }" :class="state.infomenu ? 'menu-off': 'active-link' " class="nav-link" @click="state.updateActvPage(4)" >contatti</router-link>
      <router-link :to="{ name: 'prenota' }" :class="state.infomenu ? 'menu-off': 'active-link' " class="nav-link" @click="state.updateActvPage(5)" >Ordina d'Asporto</router-link>
      <router-link :to="{ name: 'prenotaServizio' }" :class="state.infomenu ? 'menu-off': 'active-link' " class="nav-link" @click="state.updateActvPage(6)" >Prenota tavolo</router-link>
      
      
    </div>
    
  </div>
</template>


<style lang="scss" scoped>
@use '../assets/styles/general.scss' as *;
// .nav{
//   width: 100%;
//   height: 100%;
//   display: flex;

//   .left-nav{
//     min-width: 30%;
//     display: flex;
//     justify-content: center;
//     img{
//       height: auto;
//       width: auto;
//     }
//   }
  

//   .right-nav{
//     width: 70%;
//     background-color: #523333;
//     .link{
//       height: 100%;
      
//       display: flex;
//       justify-content: space-between;
//       align-items: center;

//     }
//   }
// }

.nav{
  background-color: white;
  display: flex;
  width: 100%;
  height: 230px;
  position: fixed;
  top: 0;
  left: 0;
  .left-nav{
    height: 100%;
    @include dfc;
    img{
      width: 200px;
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
      width: 80%;
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
      width: 65%;
      img{
        height: 100%;
      }
      .menu{
        background-color: #712A2A;
        width: 100%;

      }
    }
    .nav3{
      display: flex;
      height: 40px;
      width: 65%;
      img{
        height: 100%;
      }
      .right-nav3{
        background-color: #523333;
        width: 100%;

      }
    }
    .nav4{
      display: flex;
      height: 70px;
      width: 50%;
      img{
        height: 100%;
      }
      
      .left-nav4{
        display: flex;
        .chi-siamo{
          @include dfc;
          color: black;
          background-color: #270000;
          border-top: 8px solid white;          
          border-bottom: 8px solid white;          
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
          color: black;
          background-color: #270000;
          border-top: 8px solid white;          
          border-bottom: 8px solid white;         
          border-right: 8px solid white; 
        }
      }
    
    }
  }
}
.nav-mb-on{
  position: fixed;
  top: 0;
  left: 0;
  z-index: 10;
  background-color: #270000;
  width: 100%;
  height: 100%;
  transition: all .3s linear;
}
.burger-close-on{
  transition: all 1s linear 2s;
  position: absolute;
  top: 8%;
  right: 8%;
  opacity: 1;
  transition: display .3s linear;
  transition: opacity 1s linear 2s;
  .line{
    background-color: white;
    height: 30px;
    width: 5px;
    transform: rotateZ(45deg);
    position: absolute;
  }
  .l1{
    transform: rotateZ(135deg)
  }
}
.top-on{
  @include dfc;
  height: 100%;
  justify-content: space-around;
  flex-direction: column;
  padding: 10%;
  opacity: 1 ;
  transition: display .3s linear 1s;
  transition: opacity 5s linear 2s;
  .nav-link{

    text-transform: uppercase;
    line-height: 2rem;
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



</style>


