<template>
  <div id="app">
    <input type="number" v-model.number="limit" min="1" max="100"/>
    <Numbers :number="getLimit"/>
  </div>
</template>

<script>
import Numbers from '@/components/Numbers';

export default {
  name: 'App',
  components: {Numbers},
  data()
  {
    return {
      limit: 100
    }
  },
  computed: {
    getLimit(){
      if (this.limit < 1 ){
        return this.limit = 1
      } else {
        return this.limit
      }
    }
  }
}
</script>

<style scoped>
</style>
