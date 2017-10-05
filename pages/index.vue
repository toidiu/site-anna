<template>
  <section class="section">
    <div>
      <h1 class="title">
        mta-status
      </h1>
      <h2 class="subtitle">
        blo
        {{ $store.state.mta.timestamp }}
        </br>
        bla
        {{ $store.state.counter }}
        </br>
        blu
        {{ timestamp }}
      </h2>
      <div class="links">
        <a @click="$store.commit('increment')"  class="button is-primary">Count</a>
      </div>
    </div>
  </section>
</template>

<script>
import axios from 'axios'

export default {
  data () {
    return { timestamp: 'default' }
  },
  components: {
  },
  asyncData (context) {
    return { timestamp: 'now' }
  },
  async fetch ({ store, params }) {
    try {
      let { data } = await axios.get('http://localhost:4000')
      store.commit('setMta', data)
    } catch (e) {
      this.errors.push(e)
    }
  }
}
</script>

<style>



</style>
