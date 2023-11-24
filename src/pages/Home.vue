<script >
import { state } from '../state.js'
import axios from 'axios';
import AppNav from '../components/AppNav.vue'


export default {
    components: { AppNav, },

    data() {
        return {
            state,
            obs: 0,
        }
    },
    created() {
        axios.get(state.baseUrl + 'api/setting', {}).then(response => this.state.setting = response.data.results);

        this.state.actvPage = 1;
    },
    methods: {

    }


}
</script>

<template>

    <div class="home">
        <div class="home-left">
            <img src="../assets/img/sushibac.png" alt="" class="sushi">
        </div>
        <div class="home-right">
            <h1>SCOPRI LA VERA CUCINA ORIENTALE E PROVA IL NOSTRO SUSHI</h1>
            <p>SOLO SUL NOSTRO SITO UFFICIALE PUOI TROVARE IL NOSTRO MENU, PRENOTARE UN TAVOLO O ADDIRITTURA PRENOTARE IL
                TUO ASPORTO</p>
            <router-link :to="{ name: 'menu' }" class="btn">Menu</router-link>

        </div>
    </div>

    <div class="home-respo">
        <div class="main">
            <h1>SCOPRI LA VERA CUCINA ORIENTALE E PROVA IL NOSTRO SUSHI</h1>
            <img src="../assets/img/sushibac.png" alt="" class="sushi-respo">
            <p>SOLO SUL NOSTRO SITO UFFICILAE PUOI TROVARE IL NOSTRO MENU, PERNOTARE UN TAVOLA O ADDIRITTURARA PRENOTARE IL
                TUO ASPORTO</p>
            <router-link :to="{ name: 'menu' }" class="btn">Menu</router-link>
        </div>
    </div>
</template>

<style scoped lang="scss">
@use '../assets/styles/general.scss' as *;

* {
    font-family: 'Gabarito', cursive;
}

.main-home::-webkit-scrollbar {

    width: 10px;
    height: 10px;

}

.main-home::-webkit-scrollbar-thumb {
    border-radius: 20px;
    background: $c-header;

}

.main-home::-webkit-scrollbar-track {
    border-radius: 20px;
    background: rgba(52, 4, 7, 0.786);

}

.main-home::-webkit-scrollbar-thumb:hover {
    border-radius: 20px;
    background-color: $c-nav-link;
    border: 2px solid $c-header;

}
.home-respo{
    display: none;
}
.home {
    margin-top: 230px;
    background-color: #270000;
    width: 100%;
    display: flex;
    

    .home-left {
        display: flex;
        align-items: center;
        justify-content: center;
        padding-left: 300px;
        width: 50%;
        position: relative;

        .sushi {
            

        }

       

    }

    .home-right {
        font-size: 25px;
        width: 40%;
        height: 90%;
        padding-top: 70px;
        display: flex;
        flex-direction: column;
        justify-content: space-between;

        p {
            width: 70%;
            align-self: flex-end;
            font-size: 20px;
        }

        .btn {
            width: 200px;
            padding: 20px 0;
            border-radius: 50px;
            display: flex;
            justify-content: center;
            align-self: center;
            font-size: 25px;
            background-color: #523333;
            border: 5px solid white;
        }
    }

}


// @media (max-width:1600px) {
    
//     .sushi {
            
//         min-width: 800px;

//         }
// }
// @media (max-width:1350px) {
    
//     .home{
//         h1{
//             font-size: 45px;
//         }
//         .home-left{
//             padding-left: 100px;
//             .sushi {
                    
//                 min-width: 700px;
        
//                 }
//         }
//     }
// }
// @media (max-width:1000px) {
    
//     .home{
//         h1{
//             font-size: 40px;
//         }
//         p{
//             font-size: 15px!important;

//         }
//         .home-left{
//             padding-left: 100px;
//             .sushi {
                    
//                 min-width: 600px;
        
//                 }
//         }
//     }
// }

// @media (max-width:900px) {
    
//     .home{
//         display: none;
//     }
//     .home-respo{
//         background-color: #270000;
//         height: 70%;
//         width: 100%;
//         margin: auto;
//         position: fixed;
//         bottom: 0;
//         display: flex;
//         justify-content: center;
//         align-items: center;
//         text-align: center;
        
//         .main{
//             width: 90%;
//             margin: auto;
//             display: flex;
//             flex-direction: column;
//             align-items: center;
//             justify-content: center;
//             .sushi-respo{
//                 width: 500px;
//             }
//         }

//         .btn{
//             margin-top: 2rem;
//         }
//     }
// }




</style>
