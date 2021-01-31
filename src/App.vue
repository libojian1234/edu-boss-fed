<template>
  <div id="app">
    <!-- 根路由出口 -->
    <router-view/>
  </div>
</template>

<!--<script lange="ts">
import Vue from 'vue'
import Component from 'vue-class-component'
@Component
export default class App extends Vue {
  a = 1
  b = '2'
  c = {
    a: 1,
    b: '2'
  }

  test () {
    console.log(this.a)
  }
}
</script>
-->
<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
  name: 'App'
})
</script>
<style lang="scss" scoped></style>
