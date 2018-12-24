<template>
  <section class="container">
      <Top />
      <Nav />
  </section>
</template>

<script>
import axios from 'axios'
import indexCss from '~/assets/index.css'
import Top from '~/components/top.vue'
import Nav from '~/components/Navigation.vue'


export default {
  components: {
    Top,Nav
  }
}
</script>

