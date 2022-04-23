<template>
  <div id="app">
    <input type="number" v-model="limit" />
    <NumbersDisplay/>
  </div>
</template>

<script>
import NumbersDisplay from '@/components/NumbersDisplay';

export default {
  name: 'App',
  components: {NumbersDisplay},
  data()
  {
    return {
      limit: 100
    }
  }
}
</script>

<style scoped>

  /* Made some minor overall styling improvements */

  #app {
    padding: 2rem;
    text-align: center;
  }

  input {
    margin-bottom: 2rem;
    padding: 0.3rem;
    border: 2px solid black;
    border-radius: 8px;
    font-weight: 600;
  }

</style>
