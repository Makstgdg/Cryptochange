<template>
<h1>CRYPTO</h1>
  <Input :changeAmount = "changeAmount" :convert="convert"/>
  <p v-if="errors !== ''">{{errors}}</p>
  <p class="resultHere" v-if="result !== 0">{{amount}} {{cryptoFirst}} это {{result}} {{cryptoSecond}}</p>
  <div class="selectBlock">
  <Selector :setCrypto="setCryptoFirst"/>
  <Selector :setCrypto="setCryptoSecond"/>
  </div>
</template>

<script>
import Input from "@/components/input.vue";
import Selector from "@/components/Selector.vue";
import CryptoConvert from "crypto-convert";

const convert = new CryptoConvert();
export default {
  components: {Input , Selector},
  data(){
    return{
      amount: 0,
      cryptoFirst: "",
      cryptoSecond: "",
      errors: "",
      result: 0,
    }
  },
  methods:{
    changeAmount(val){
      this.amount = val;
    },
    setCryptoFirst(val){
      this.cryptoFirst = val;
    },
    setCryptoSecond(val){
      this.cryptoSecond = val;
    },
    async convert(){
      if(this.amount <= 0){
        this.errors = "Введите число больше 0";
        return;
      }
      else if(this.cryptoFirst === '' || this.cryptoSecond === ''){
        this.errors = "Выберите валюту";
        return;
      }
      else if(this.cryptoFirst === this.cryptoSecond){
        this.errors = "Конвертация одинаковой валюты невозможна";
        return;
      }
      else{
        this.errors = '';
      }
      await convert.ready(); //Wait for the initial cache to load

      if(this.cryptoFirst === 'BTC' && this.cryptoSecond === 'ETH'){
      this.result = convert.BTC.ETH(this.amount).toFixed(2);
      }
      if(this.cryptoFirst === 'BTC' && this.cryptoSecond === 'DOGE'){
        this.result = convert.BTC.DOGE(this.amount).toFixed(2);
      }
      if(this.cryptoFirst === 'ETH' && this.cryptoSecond === 'BTC'){
        this.result = convert.ETH.BTC(this.amount).toFixed(2);
      }
      if(this.cryptoFirst === 'ETH' && this.cryptoSecond === 'DOGE'){
        this.result = convert.ETH.DOGE(this.amount).toFixed(2);
      }
      if(this.cryptoFirst === 'DOGE' && this.cryptoSecond === 'BTC'){
        this.result = convert.DOGE.BTC(this.amount).toFixed(2);
      }
      if(this.cryptoFirst === 'DOGE' && this.cryptoSecond === 'ETH'){
        this.result = convert.DOGE.ETH(this.amount).toFixed(2);
      }
    }
  }
}

</script>

<style scoped>
.selectBlock{
  display: flex;
  justify-content: space-around;
  width: 30%;
  margin: 25px auto;
}
h1{
  text-align: center;
  margin-top: 5%;
  font-size: 75px;
  font-family: "Nabla", system-ui;
  font-optical-sizing: auto;
  font-weight: 400;
  font-style: normal;
  font-variation-settings:
      "EDPT" 100,
      "EHLT" 12;
}
.resultHere{
  background: #1a032d;
  color: white;
  padding: 15px 20px;
  margin: 15px auto;
  text-align: center;
  width: 20%;
  border-radius: 3px;

}
</style>
