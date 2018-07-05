<template>
  <div class="home">
    <Navbar></Navbar>
    <Articles></Articles>
  </div>
</template>

<script>
// @ is an alias to /src
import Navbar from '@/components/Navbar.vue'
import Articles from '@/components/Articles.vue'
export default {
  name: 'home',
  components: {
    Navbar,
    Articles
  }
}
</script>
