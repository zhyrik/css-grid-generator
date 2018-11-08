<template>
  <div id="app">

    <div class="writen-wrap">
      <label for="colums">grid-template-columns</label>
      <input type="text" v-model="columns" id="columns">

      <label for="rovs">grid-template-rows</label>
      <input type="text" v-model="rows" id="rows">

      <label for="gap">grid-gap</label>
      <input type="text" v-model="gap" id="gap">
    </div>

    <div class="container" :style="container">
      <div class="items" v-for="item in 400" :key="item"></div>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      columns: '20% 20% 20% 20% 20%',
      rows: '20% 20% 20% 20% 20%',
      gap: '0% 0%'
    }
  },
  computed: {
    container () {
      return {
        'grid-template-columns': this.columns,
        'grid-template-rows': this.rows,
        'grid-gap': this.gap
      }
    }
  },
  name: 'App'
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  display: flex;
  justify-content: space-around;
}
.writen-wrap{
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  justify-content: flex-start;
}
.container{
  width: 500px;
  height: 500px;
  display: grid;
  grid-template-rows: 20% 20% 20% 20% 20%;
  background: red;
  border: 2px solid black;
  overflow: hidden;
  position: relative;
}
.items{
  border: 1px solid black;
}
input{
  width: 400px;
  padding: 5px 20px;
  margin-bottom: 20px;
  margin-top: 5px;
}
</style>
