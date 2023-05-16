<template>
  <div>
    <Navbar />
    <div class="container">
      <router-view />
    </div>
  </div>
</template>

<script>
import Navbar from "./components/Navbar.vue"
import "materialize-css/dist/css/materialize.min.css"
import "materialize-css/dist/js/materialize.min.js"

export default {
  components: {
    Navbar
  }
}
</script>

<style scoped>
</style>
