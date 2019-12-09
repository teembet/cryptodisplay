<template>
  <div id="app">
    <crypto-form :cryptos="cryptos"/>
  </div>
</template>

<script>
import CryptoForm from './components/CryptoForm.vue'

export default {
  name: 'app',
  components: {
    CryptoForm
  },
   data() { 
     
            return {
             cryptos:[],
         
            }
        },

          mounted() {
            this.getCrypto()
        },

         methods: {
            async getCrypto() {
                try {
                    const response = await fetch('https://api.coinlore.com/api/tickers/')
                    const data = await response.json()
                    this.cryptos = data.data
                } catch (error) {
                    /* eslint-disable */
                    console.error(error)
                }
            },

},


}
</script>

<style>
#app{
  margin-top: 30px;
   font-size: 15px;
  line-height: 1.4;
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Oxygen-Sans, Ubuntu, Cantarell, sans-serif;
}
</style>
