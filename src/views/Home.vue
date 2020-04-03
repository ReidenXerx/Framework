<template>
  <div class="home">
    <HelloWorld msg="Welcome to Your Vue.js App"/>
    <Droplist :values="values" :title="title"/>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'
import Droplist from '@/components/Droplist.vue'

export default {
  name: 'Home',
  components: {
    HelloWorld,
    Droplist
  },
  data () {
    return {
      values: ['v1', 'v2'],
      title: 'test'
    }
  }
}
</script>
