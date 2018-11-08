<template>
  <div id="app">

    <div class="writen-wrap">
      <label for="colums">grid-template-columns (px, %, fr, repeat(n, %)</label>
      <input type="text" v-model="columns" id="columns">

      <label for="rovs">grid-template-rows</label>
      <input type="text" v-model="rows" id="rows">

      <label for="gap">grid-gap</label>
      <input type="text" v-model="gap" id="gap">

      <label for="items">Items</label>
      <input type="number" v-model="items" id="items">

      <div class="items-imput" v-for="item in numberItems" :key="item" v-if="itemsInput[item-1]">
        <label for="column">grid-column</label>
        <input type="text" v-model="column[item-1]" id="column" @input="pushItemStyle(item-1)">

        <label for="row">grid-row</label>
        <input type="text" v-model="row[item-1]" id="row" @input="pushItemStyle(item-1)">
      </div>
    </div>

    <div class="container container-relative" :style="container">
      <div class="container container-absolute" :style="container">
        <div
          class="items-green"
          v-for="item in numberItems"
          :key="item"
          :style="itemsStyle[item-1]"
          @click="showItemsInput(item-1)"
        >{{item}}</div>
      </div>
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
      gap: '0% 0%',
      items: 0,
      column: ['1 3', '2 3', '3'],
      row: ['3', '1', '2'],
      itemsStyle: [],
      itemsInput: [true, false, false]
    }
  },
  methods: {
    pushItemStyle (item) {
        this.itemsStyle[item] = {
          'grid-column': this.column[item],
          'grid-row': this.row[item]
        }
        console.log(this.itemsStyle)
    },
    showItemsInput (item) {
      for(let i = 0; i < this.items; i++){
        this.itemsInput[i] = false
        this.itemsInput[item] = true
      }
      console.log(this.itemsInput)
    }
  },
  computed: {
    container () {
      return {
        'grid-template-columns': this.columns,
        'grid-template-rows': this.rows,
        'grid-gap': this.gap
      }
    },
    // itemsStyle () {
    //   return {
    //     'grid-column': this.column,
    //     'grid-row': this.row
    //   }
    // },
    numberItems () {
      return +this.items
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
}
.container-relative{
  background: red;
  overflow: hidden;
  position: relative;
  border: 2px solid black;
}
.container-absolute{
  position: absolute;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
}
.items{
  border: 1px solid black;
}
.items-green{
  background: green;
  border: 1px solid white;
  line-height: 100px;
}
input{
  width: 400px;
  padding: 5px 20px;
  margin-bottom: 20px;
  margin-top: 5px;
}
.items-imput{
  border: 1px solid black;
  display: flex;
  flex-direction: column;

}
</style>
