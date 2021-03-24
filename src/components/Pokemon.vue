<template>
    <div id="pokemon">
        <div id="botao">
            <div v-if="solo">
                <button @click="alterarSprite">{{n+1}}</button>
            </div>
            <div v-else>
                
            </div>
        </div>
        <div id="pokeFoto">
            <img :src=info.foto>
        </div>
        <div id="pokeData">
            <h1>{{name | maiuscular}}</h1>
            <p>Type: {{info.type}}</p>
        </div>
    </div>
</template>

<script>

import axios from 'axios';

export default {
    
    created: function() {
        axios.get(this.url).then(res => {
            // console.log(res);
            this.info.type = res.data.types[0].type.name;
            this.info.imagemFrente = res.data.sprites.front_default;
            this.info.imagemCostas = res.data.sprites.back_default;
            this.info.foto = this.info.imagemFrente;
            // console.log(this.info);
        });
    },

    data() {
        return {
            info: {
                foto: '',
                type: '',
                imagemFrente: '',
                imagemCostas: ''
            }
        }
    },

    props: {
        n: Number,
        name: String,
        url: String,
        solo: Boolean
    },

    filters: {
        maiuscular: function(value) {
            return value[0].toUpperCase(0) + value.slice(1);
        }
    },

    methods: {
        alterarSprite: function() {
            if (this.info.foto == this.info.imagemFrente) {
                this.info.foto = this.info.imagemCostas
            } else {
                this.info.foto = this.info.imagemFrente
            }
        }
    }

}
</script>

<style>

    #pokemon {
        background: white;
        border-radius: 10px;
        margin: 25px 55px;
        padding: 15px;
        width: 200px;
        height: 250px;
        box-shadow: 5px 5px 15px rgba(0, 0, 0, 0.250);
    }

    @media screen and (max-width: 1021px) {
        #pokemon {
            margin: 25px 35px;
        }
    }

    @media screen and (max-width: 901px) {
        #pokemon {
            width: 160px;
            height: 210px;
            margin: 25px 25px;
        }
    }

    @media screen and (max-width: 751px) {
        #pokemon {
            width: 140px;
            height: 190px;
            margin: 15px 15px;
        }
    }

    @media screen and (max-width: 631px) {
        #pokemon {
            width: 100px;
            height: 150px;
            margin: 15px 15px;
            font-size: 12px;
        }
        #pokemon #pokeData h1 {
            font-size: 14px;
        }
        #pokemon #botao button {
            padding: 5px 8px;
            font-size: 14px;
        }
        #pokemon #pokeFoto img {
            padding-top: 10px;
        }
    }

    @media screen and (max-width: 481px) {
        #pokemon {
            padding: 5px;
            width: 95px;
            height: 142px;
            margin: 10px 10px;
            font-size: 12px;
        }
        #pokemon #pokeData h1 {
            font-size: 12px;
        }
        #pokemon #botao button {
            padding: 5px 8px;
            font-size: 12px;
        }
        #pokemon #pokeFoto img {
            padding-top: 10px;
        }
    }

    @media screen and (max-width: 376px) {
        #pokemon {
            padding: 5px;
            width: 110px;
            height: 160px;
            margin: 15px 15px;
            font-size: 12px;
        }
        #pokemon #pokeData h1 {
            font-size: 12px;
        }
        #pokemon #botao button {
            padding: 5px 8px;
            font-size: 12px;
        }
        #pokemon #pokeFoto img {
            padding-top: 10px;
        }
    }

    #pokemon img {
        width: 100%;
    }

    #pokemon h1 {
        font-size: 22px;
    }

    #pokeFoto {
        text-align: center;
    }

    #pokeData {
        text-align: center;
    }

    #botao {
        position: absolute;
    }

    #botao button {
        padding: 5px 10px;
        font-size: 20px;
        border-radius: 5px;
        border: none;
        background:  #3761A8;
        color: white;
        font-weight: bolder;
    }

    #botao button:hover {
        cursor: pointer;
        transform: scale(1.1);
    }

    #botao button:focus {
        outline-style: none;
    }

</style>