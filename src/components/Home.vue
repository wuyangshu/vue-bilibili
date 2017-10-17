<template>
  <div id="home">
    <v-header></v-header>
    <v-tabs></v-tabs>    
  </div>
</template>
<script>
import vHeader from '@/components/Header.vue'
import vTabs from '@/components/Tabs.vue'
export default {
  name: 'home',
  components: {
  "v-header":vHeader,
  "v-tabs":vTabs
  }
}

</script>

<style scoped>
body {
  background-color: #f1f1f1;
}
</style>
