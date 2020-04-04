<template>
  <table class="sexy-list">
    <caption class="sexy-caption" v-if="table_name!=''">{{table_name}}</caption>
      <tr class="sexy-head-line">
        <td class="sexy-cell" v-for="cap in table_captions" v-bind:key="cap">{{cap}}</td>
      </tr>
      <tr class="sexy-head-line">
        <td class="sexy-cell" v-for="(cell, index) in cells" v-bind:key="index"><input type="text" v-model="cell.value"/></td>
        <td class="sexy-cell"><button v-on:click="addData">Добавить</button></td>
      </tr>
      <tr v-for="(item, index) in table_data"  v-bind:key="index" class="sexy-line">
        <td class="sexy-cell" v-for="(cell, index) in item"  v-bind:key="index">{{cell}}</td>
        <td class="sexy-cell"><button v-on:click="removeData(index)">Удалить</button></td>
      </tr>
  </table>

</template>

<script>
export default {
  name: 'sexyTable',
  props: {
    table_data: {
      type: Array,
      default: function () { return [{ c1: 'i1', c2: 'i2' }] }
    },
    table_name: {
      type: String,
      default: ''
    },
    table_captions: {
      type: Array,
      default: function () { return ['cap1', 'cap2', '', ''] }
    }
  },
  data () {
    return {
      cells: []
    }
  },
  mounted: function () {
    var elems = Object.values(this.table_data[0])
    for (var i = 0; i < elems.length; i++) {
      this.cells.push({ value: elems[i] })
    }
  },
  methods: {
    addData: function () {
      var buf = Object.assign({}, this.table_data[0])
      console.log(buf)
      var i = 0
      for (var key in buf) {
        buf[key] = this.cells[i++].value
      }
      console.log(buf)
      this.table_data.push(buf)
    },
    removeData: function (i) {
      this.table_data.splice(i, 1)
    },
    renameTable: function (name) {
      this.table_name = name
    }

  }
}
</script>
<style media="screen">
table {
    background: red;
    /* TODO: fonts and etc */
}
</style>
