<template>
  <div id="app">

    <div class="writen-wrap">
      <div class="writen-wrap__container">
        <h4>.container</h4>
        <div>
          <label for="columns">grid-template-columns</label>
          <input
            type="text"
            v-model.trim="columns"
            id="columns"
            title="px, %, fr, em, auto, repeat(n, fr), min-content, max-content, minmax">
        </div>

        <div>
          <label for="rows">grid-template-rows</label>
          <input
            type="text"
            v-model.trim="rows"
            id="rows"
            title="px, %, fr, em, auto, repeat(n, fr), min-content, max-content, minmax">
        </div>

        <div>
          <label for="gap">grid-gap</label>
          <input
            type="text"
            v-model.trim="gap"
            id="gap"
            title="px, %, fr, em, auto">
        </div>
      </div>

      <label for="items">Create items (max {{countItems}})</label>
      <input type="number" v-model="items" id="items">

      <span>Click on the green block for change number item</span>
      <div class="writen-wrap__item" v-for="item in numberItems" :key="item" v-if="itemsInput[item-1]">
        <h4>.item{{item}}</h4>
        <div>
          <label for="column">grid-column</label>
          <input type="text" v-model="column[item-1]" id="column" @input="pushItemStyle(item-1)">
        </div>

        <div>
          <label for="row">grid-row</label>
          <input type="text" v-model="row[item-1]" id="row" @input="pushItemStyle(item-1)">
        </div>

        <div>
          <label for="order">order</label>
          <input
            type="text"
            v-model="order[item-1]"
            id="order" @input="pushItemStyle(item-1)"
            title="--1, 1++">
        </div>
      </div>
      <button @click="getCode">get code</button>
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
      <div class="items" v-for="(item, index) in countItems" :key="index"></div>
    </div>

    <div class="modal" v-if="modal">
      <div v-text="modalText"></div>
      <div>
        <button @click="modal=!modal">close</button>
        <a href="https://github.com/zhyrik/css-grid-generator"
          target="_blank"
          class="button"
        >support project add star on github</a>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      columns: '20% 1fr 100px 20% 20%',
      rows: '1fr 2fr 10%',
      gap: '0% 0%',
      items: 1,
      column: [],
      row: [],
      order: [],
      itemsStyle: [],
      itemsInput: [true, false, false],
      modal: false,
      modalText: ''
    }
  },
  methods: {
    pushItemStyle (item) {
        this.itemsStyle[item] = {
          'grid-column': this.column[item],
          'grid-row': this.row[item],
          'order': this.order[item]
        }
    },
    showItemsInput (item) {
      for(let i = 0; i < this.items; i++){
        this.$set(this.itemsInput, i, false)
        this.$set(this.itemsInput, item, true)
      }
    },
    getCode () {
      let container = `
  .container{
  \t'grid-template-columns': ${this.columns},
  \t'grid-template-rows': ${this.rows},
  \t'grid-gap': ${this.gap}
  } \n`
      let items = ''
      for(let i = 0; i < this.itemsStyle.length; i++) {
        if(this.itemsStyle[i]) {
          items += '\n item' + i + " {"
          if(this.itemsStyle[i]['grid-column'] !== undefined) items += '\n \tgrid-column: ' + this.itemsStyle[i]['grid-column'] + ';'
          if(this.itemsStyle[i]['grid-row'] !== undefined) items += '\n \tgrid-row: ' + this.itemsStyle[i]['grid-row'] + ';'
          if(this.itemsStyle[i]['order'] !== undefined) items += '\n \torder: ' + this.itemsStyle[i]['order'] + ';'
          items += '\n }'
        }
      }
      this.modalText = container + items
      this.modal = !this.modal
      console.log(this.container, items)
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
    countItems () {
      return (this.columns.match(/\s+/g).length + 1) * (this.rows.match(/\s+/g).length + 1)
    }, 
    numberItems () {
      return +this.items
    }
  },
  name: 'App'
}
</script>

<style>
h1{
  text-align: center;
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  margin-top: 10px;
  display: flex;
  justify-content: space-around;
}
h4{
  margin: 0;
}
.writen-wrap{
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  justify-content: flex-start;
}
.writen-wrap__container{
  width: 550px;
  padding: 10px ;
  border: 1px solid black;
  margin-bottom: 20px;
}
.writen-wrap__container div{
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.container{
  width: 500px;
  height: 500px;
  display: grid;
}
.container-relative{
  background: rgba(221, 160, 74, 0.952);
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
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  transition: all 0.3s;
}
.items-green:hover{
  background: greenyellow;
}
input{
  width: 300px;
  padding: 5px 20px;
  margin: 5px 0;
}
.writen-wrap__item{
  padding: 10px ;
  border: 1px solid black;
  display: flex;
  flex-direction: column;
  width: 550px;

}
.writen-wrap__item div{
  display: flex;
  justify-content: space-between;
  align-items: center;
}
label{
  cursor: pointer;
}
span{
  margin-top: 10px;
}
.modal{
  position: fixed;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  background: rgba(226, 216, 202, 0.952);
  display: flex; 
  flex-direction: column;
  align-items: center;
}
.modal div{
  white-space: pre;
}
button, .button{
  border: 2px solid black;
  cursor: pointer;
  padding: 10px 40px;
  margin: 0 auto;
  text-transform: uppercase;
  background: rgba(221, 160, 74, 0.952);
  font-size: 16px;
  text-decoration: none;
  color: black;
  margin: 10px; 
}
button:hover, .button:hover{
  background: rgba(224, 192, 146, 0.952);
}
</style>
