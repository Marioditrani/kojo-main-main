<script >
  import {state} from '../state.js'
  import sh from '../components/SHeader.vue'

  export default {
    components:{sh},
    data(){
        return{     
            state,
         //center: {lat: 51.093048, lng: 6.842120},
            
        }
    },
    created(){
      this.state.actvPage = 4;
    }
    
  }
</script>

<template>
  <sh/>
  <div class="contatti">
    <div class="cont">
      <div class="card1">
        <div class="card1-left">
          <img src="../assets/img/sushi.png" alt="" class="sushi">
            <img src="../assets/img/crop.png" alt="" class="bac">
        </div>
        <div class="card1-right">
          <h1>CONTATTI</h1>
          <div class="bottom">
            <span class="tel">TELEFONO</span>
            <span>+39 333 232 1234</span>
            <span class="tel">EMAIL</span>
            <span>LATUAMAIL@GMAIL.COM</span>

          </div>
        </div>
      </div>
      <div class="card2">
        <div class="card2-left">
          <div class="topinfo" >
            <h4>Orari d'apertura</h4>
            <div class="sec-1">
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
            
          </div>
        </div>
        <div class="card2-right">
            <h1>DOVE TROVARCI</h1>
            <a href="https://www.google.com/maps/place/Kojo+Sushi/@43.5855969,13.308124,17.75z/data=!4m6!3m5!1s0x132d9d63861ba9c3:0x9a352a43c5be1c0e!8m2!3d43.5851992!4d13.3073426!16s%2Fg%2F11kjgq2ccy?hl=it&entry=ttu"><img src="../assets/img/maps.png" alt=""></a>
        </div>

      </div>
      
    </div>
  </div>
</template>

<style scoped lang="scss">
@use '../assets/styles/general.scss' as *;

.contatti::-webkit-scrollbar{
      
      width: 10px;
      height: 10px;
      
  }

.contatti::-webkit-scrollbar-thumb {
    border-radius: 20px;
    background: $c-header;
    
}
.contatti::-webkit-scrollbar-track {
    border-radius: 20px;
    background: rgba(52, 4, 7, 0.786);
    
}
.contatti::-webkit-scrollbar-thumb:hover {
    border-radius: 20px;
    background-color: $c-nav-link;
    border: 2px solid $c-header;
    
}


img{
  width: 100%;
  max-width: 600px;
}
.contatti{
  overflow: auto;
  background-color: #270000;
  position: fixed;
    bottom: 0;
    left: 0;
    height: 69%;
    width: 100%;

  .cont{
    
    width: 90%;
    height: 100%;
    margin: auto;

    .card1{
      padding-top: 50px;
      display: flex;
      .card1-left{
        width: 50%;
        position: relative;
        
        .sushi{
          max-width: 400px;
            position: absolute;
            left: 30%;
            top: 15%;
            
        }
        .bac{
            max-width: 200px;
            position: absolute;
            left: 70%;
            top: 30%;
            transform: rotate(-40deg);
        }
      }

      .card1-right{
        width: 50%;
        text-align: center;
        display: flex;
        flex-direction: column;
        h1{
          font-size: 50px;
        }

        .bottom{
          padding-top: 60px;
          display: flex;
          flex-direction: column;
          gap: 30px

          
        }
      }
    }

    .card2{
      padding-top: 150px;
      display: flex;
      .card2-left{
        width: 50%;
        text-align: center;
        
        .topinfo{
          font-size: 50px;
          display: flex;
          flex-direction: column;
          align-items: center;
          gap: 40px;
          .sec-1{
            width: 50%;
            font-size: 20px;
            display: flex;
            justify-content: space-between;
            .cont-giorni{
              display: flex;
              flex-direction: column;
              gap: 10px;
            }
            .cont-orari{
              display: flex;
              flex-direction: column;
              gap: 10px;
            }
          }
        }
      }
      .card2-right{
        width: 50%;
        text-align: center;
        padding-top: 300px;

        img{
          padding: 20px 0;
          max-width: 500px;
        }
      }
    }
    
  }

}
.bottom{
  padding-left: 100px;
  text-align: start;
  span{
       font-size: 20px;
       }
}

.map{
  @include dfc;
  flex-direction: column;
  gap: 1rem;
  img{
    width: 90%;
  }
}


@media (max-width:$bp1) {.btn-menu{display:block;}}

</style>
