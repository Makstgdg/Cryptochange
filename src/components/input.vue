<template>
  <input min="0" type="number" @input="changeAmount($event.target.value)">
 <br>
  <button @click="convert()">Конвертировать</button>
</template>

<script>
export default {
  props:{
    changeAmount: {
      type: Function, required: true,
    },
    convert:{
      type: Function, required: true,
    }
  }
}
</script>

<style scoped>
input{
  width: 250px;
  border-radius: 10px;
  border: 0;
  padding: 10px 15px;
  background: #fafafa;
  color: black;
}
button{
  position: relative;
  padding: 15px 20px;
  top: 20px;
  margin: 15px 0;
  text-transform: uppercase;
  cursor: pointer;
  background: #1a032d;
  color: white;
  border: 0;
  border-radius: 3px;
}
</style>
