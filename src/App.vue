<template>
    <h1>CRYPTO</h1>
    <Input :changeAmount="changeAmount" />
    <p v-if="error != ''" class="error">{{ error }}</p>
    <Favourite :favourites="favourites" :getFromFavourites="getFromFavourites" v-if="favourites.length > 0" />
    
    <div class="selectors">
        <Selector :setCrypto="setCryptoFirst" :cryptoNow="cryptoFirst" />
        <Selector :setCrypto="setCryptoSecond" :cryptoNow="cryptoSecond" />
    </div>
    <input type="number" class="inputResult" v-model="info" placeholder="Resultado de la conversión" readonly />
    <button class="buttonConvert" @click="convert()">Convertir</button>
    <button class="buttonConvert" @click="favourite()">Añadir a favoritos</button>

</template>



<script>
import Favourite from "./components/Favourite.vue"
import Input from "./components/Input.vue"
import Selector from "./components/Selector.vue"
import axios from "axios"

export default {
    components: { Input, Selector, Favourite },
    data() {
        return {
            amount: 0,
            cryptoFirst: "",
            cryptoSecond: "",
            error: "",
            info: null,
            favourites: []
        }
    },
    methods: {
        getFromFavourites(index) {
            this.cryptoFirst = this.favourites[index].from
            this.cryptoSecond = this.favourites[index].to
        },

        favourite() {
            if(this.cryptoFirst == this.cryptoSecond) {
                this.error = "Seleccione criptomonedas diferentes"
                return;
            }
            this.error = ""

            this.favourites.push({
                from: this.cryptoFirst,
                to: this.cryptoSecond
            });
            
        },

        changeAmount(val) {
            this.amount = val
        },
        setCryptoFirst(val) {
            this.cryptoFirst = val
        },
        setCryptoSecond(val) {
            this.cryptoSecond = val
        },

        convert() {
            this.errorMessage()
            if(this.error) {
                return; // Finalizar ejecucion si hay un error
            }

            const apiUrl = `https://api.coinconvert.net/convert/${this.cryptoFirst}/${this.cryptoSecond}?amount=${this.amount}`
            axios.get(apiUrl)
                .then(response => {this.info = response.data[this.cryptoSecond]})
                .catch(error => {
                    console.error("Error al realizar la conversión:", error);
                    this.error = "Error al realizar la conversión";
                });
        },
        

        errorMessage() {
            if(this.amount == "") {
                this.error = "Introduce un numero"
            }
            else if(this.amount <= 0) {
                this.error = "Numero no puede ser menor o igual a 0"
            }
            else if(this.cryptoFirst == "" || this.cryptoSecond == "") {
                this.error = "Selecciona las criptomonedas"
            }
            else if(this.cryptoFirst == this.cryptoSecond) {
                this.error = "Las criptomonedas no pueden ser iguales"
            }
            else {
                this.error = ""
            }
        }
    }
}



</script>



<style scoped>
.selectors {
    display: flex;
    justify-content: space-around;
    width: 80%;
    max-width: 700px;
    margin: 0 auto;
    gap: 20px;
}

.buttonConvert {
    display: block;
    max-width: 200px;
    width: 80%;
    margin: 20px auto;
    padding: 10px;
    background: #1a032d;
    color: #fff;
    border: none;
    border-radius: 5px;
    cursor: pointer;
}
.buttonConvert:hover {
    background: #2b054a;
}

.error {
    color: red;
}

.inputResult {
    display: block;
    margin: 20px auto;
    border-radius: 5px;
    border: 0;
    padding: 8px;
    width: 80%;
    max-width: 540px;
}

.inputResult:focus {
    outline: none;
    box-shadow: none;
}


@media (max-width: 600px) {
    .selectors {
        width: 100%;
    }
}

</style>
