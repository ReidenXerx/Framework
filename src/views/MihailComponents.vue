<template lang="html">
  <div class="">
    <Droplist :values="values" :title="title"/>
    <MihailWindow :header="title" :x="600" :y="600">
      <div slot="window-body">
        <p>slot usage example</p>
        <p>for ReidenXerx</p>
      </div>
    </MihailWindow>
    <MihailWindow/>
    <DynamicTable v-if="false" />
  </div>
</template>

<script>
// @ is an alias to /src
import MihailWindow from '@/components/Window.vue'
import DynamicTable from '@/components/DynamicTable.vue'
import Droplist from '@/components/Droplist.vue'

export default {
  name: 'mihailview',
  components: {
    MihailWindow,
    DynamicTable,
    Droplist
  },
  data () {
    return {
      values: ['v1', 'v2'],
      title: 'another window'
    }
  }
}
</script>

<style lang="css" scoped>
</style>
