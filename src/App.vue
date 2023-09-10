<template>
  <router-view/>
</template>

<script lang="ts">
import {computed, reactive, defineComponent } from 'vue'
import { useHead } from '@vueuse/head'

export default defineComponent({
  setup() {
    const siteData = reactive({
      title: `Web Design Commissions`,
      description: `We specialize in building complex or simple web apps with many different tools.  Use our web commission plan builder to get a quote today!`,
    })
    useHead({
      // Can be static or computed
      title: computed(() => siteData.title),
      meta: [
        {
          name: `description`,
          content: computed(() => siteData.description),
        },
        ],
     
    })
  },
})
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  padding: 0;
}
body, html {
  margin: 0 !important;
  padding: 0 !important;
}
nav {
  padding: 30px;

  a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
</style>
