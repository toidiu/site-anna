<template>
  <section class="section">
    <div>
      <logo/>
      <h1 class="title">
        site-anna
      </h1>
      <h2 class="subtitle">
        a site for anna
      </h2>
      <div class="links">
        <a href="https://nuxtjs.org/" target="_blank" class="button is-primary">Documentation</a>
        <a href="https://github.com/nuxt/nuxt.js" target="_blank" class="button">GitHub</a>
      </div>
    </div>
  </section>
</template>

<script>
import Logo from '~/components/Logo.vue'

export default {
  components: {
    Logo
  }
}
</script>

<style>

.title {
  font-family: "Quicksand", "Source Sans Pro", -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif; /* 1 */
}


</style>
