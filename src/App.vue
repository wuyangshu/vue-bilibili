<template>
  <div id="app">
    <router-view></router-view>
    <v-navigation></v-navigation>
  </div>
</template>

<script>
import vNavigation from '@/components/Navigation.vue'
export default {
  name: 'app',
  components: {
  "v-navigation":vNavigation
  }
}

</script>

<style>
body {
  background-color: #f1f1f1;
}
</style>
