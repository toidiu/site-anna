<template>
  <section class="section">
    <div>

      <h1 class="title">
        mta-status
      </h1>

      <div class="columns is-mobile">
        <div class="column">
          <h1 class="title">local</h1>
          {{ timestamp }}
          <ul v-if="lines && lines.length">
            <li v-for="line of lines">
              <p><strong>{{line.name}}</strong></p>
            </li>
          </ul>
          <ul v-if="errors && errors.length">
            <li v-for="error of errors">
              {{error.message}}
            </li>
          </ul>
        </div>
        <div class="column">
          <h1 class="title">store</h1>
          <a v-on:click="refresh"  class="button is-primary">Refresh</a>
          </br>
          {{ $store.state.mta.timestamp }}
          <ul v-if="$store.state.mta.lines && $store.state.mta.lines.length">
            <li v-for="line of $store.state.mta.lines">
              <p><strong>{{ line.name }}</strong></p>
            </li>
          </ul>

        </div>
      </div>


      {{ $store.state.counter }}
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
    return {
      timestamp: '',
      lines: [],
      errors: []
    }
  },
  methods: {
    refresh: async function (e) {
      try {
        let { data } = await axios.get('http://localhost:4000')
        this.$store.commit('setMta', data)
      } catch (e) {
        this.errors.push(e)
      }
    }
  },
  created () {
    axios.get('http://localhost:4000')
      .then(response => {
        // JSON responses are automatically parsed.
        this.lines = response.data.lines
        this.timestamp = response.data.timestamp
      })
      .catch(e => {
        this.errors.push(e)
      })
  },
  async fetch ({ store }) {
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
