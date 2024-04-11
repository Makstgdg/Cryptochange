<template>
<ul>
  <li @click="setCurrent('BTC')" :class="current === 'BTC' ? 'active' : ''">Bitcoin</li>
  <li @click="setCurrent('ETH')" :class="current === 'ETH' ? 'active' : ''">ETH</li>
  <li @click="setCurrent('DOGE')" :class="current === 'DOGE' ? 'active' : ''">DogeCoin</li>
</ul>
</template>

<script>
export default {
  props:{
    setCrypto:{
      type:Function, required:true
    }
  },
  data(){
    return{
      current: ""
    }
  },
  methods:{
    setCurrent(val){
      this.setCrypto(val);
      this.current = val;
    }
  }
}
</script>

<style scoped>
ul{
  list-style: none;
  width: 200px;
  padding: 0;
  border-radius: 3px;
  border: 3px solid black;
}
li{
  display: block;
  background: #1a032d;
  color: #fff;
  padding: 20px 0;
  text-align: center;
}
li:hover, li.active{
  background: #24043e;
  cursor: pointer;
}
</style>
