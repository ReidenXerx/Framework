<template lang="html">
  <div class="droplist">
    <h2>{{title}}</h2>
    <div class="item head" v-on:click="toggled = !toggled">{{selected}}</div>
    <div class="" v-if="toggled">
      <div class="item" v-for="(v, index) in values" v-bind:key="index" v-on:click="selectItem(index)">
        {{v}}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'droplist',
  props: {
    values: Array,
    title: {
      type: String,
      default: () => ''
    }
  },
  data () {
    return {
      selected: '(empty)',
      toggled: false
    }
  },
  methods: {
    selectItem: function (i) {
      this.selected = this.values[i]
    }
  }
}
</script>

<style lang="scss" scoped>
$black: #2a2a2e;
$salad: #42b983;
.droplist {
  width: 80px;
  cursor: pointer;
  user-select: none;
}
.item {
  padding: 8px;
  border-bottom: 1px solid $black;
  border-left: 1px solid $black;
  border-right: 1px solid $black;

  &:hover {
    background: $salad;
  }
}
.head {
  border-top: 1px solid $black;
  background: $salad;
}
</style>
