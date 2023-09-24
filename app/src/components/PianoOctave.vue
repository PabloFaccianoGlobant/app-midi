<template>
  <div class="flex gap-x-px">
    <div class="flex gap-x-px w-auto" v-for="index in this.count" :key="index">
      <button class="key key-white"></button>
      <button class="key key-black"></button>
      <button class="key key-white"></button>
      <button class="key key-black"></button>
      <button class="key key-white"></button>   
      <div></div> 
      <button class="key key-white"></button>
      <button class="key key-black"></button>
      <button class="key key-white"></button>
      <button class="key key-black"></button>
      <button class="key key-white"></button>
      <button class="key key-black"></button>
      <button class="key key-white"></button>
      <div></div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    'count': Number
  }
}
</script>

<style scoped>
.key {
  cursor: pointer;
}

.key-white {
  width: .75rem;
  height: 5rem;
  background-color: #fff8;
}
.key-white:active {
  background-color: #fff;
}

.key-black {
  z-index: 10;
  width: .50rem;
  height: 3rem;
  margin-left: -.25rem;
  margin-right: -.25rem;
  background-color: #007ACC;
}
.key-black:active {
  background-color: #000;
}




</style>