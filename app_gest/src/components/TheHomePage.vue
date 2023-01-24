<template>
  <main>
   <TheNavbarPage :count="count"></TheNavbarPage>
   <TheProductPage @addToCard="setCount()"></TheProductPage>
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
    }
  },
  methods: {
    setCount(){
      this.count++
    }
  },
};
</script>


<style></style>
