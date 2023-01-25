<template>
  <main>
   <TheNavbarPage @loginIn="loginUp()" :count="count"></TheNavbarPage>
   <TheProductPage @addToCard="setCount()" :status="state"></TheProductPage>
  </main>
</template>


<script>

import TheNavbarPage from '../components/TheNavbarPage.vue'
import TheProductPage from '../components/TheProductPage.vue'

export default {
  components : {
    TheNavbarPage,
    TheProductPage
  },
  data() {
    return {
      count:0,
      state:false
    }
  },
  methods: {
    setCount(){
      this.count++
    },
    loginUp(){
      this.state=true
    }
  },
};
</script>


<style></style>
