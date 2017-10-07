<template>
  <section class="section">
    <div>

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

      <h1 class="title">
        mta-status
      </h1>
      {{ $store.state.counter }}
      <div class="links">
        <a @click="$store.commit('increment')"  class="button is-primary">Count</a>
      </div>

      <h2 class="subtitle">
        </br>
        {{ $store.state.mta.timestamp }}
        {{ mydata }}
        </br>
        </br>
      </h2>

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
  asyncData (context) {
    return {
      mydata: 2
    }
  },
  created () {
    // axios.get(`http://jsonplaceholder.typicode.com/posts`)
    axios.get(`http://localhost:4000`)
      .then(response => {
        // JSON responses are automatically parsed.
        this.lines = response.data.lines
        this.timestamp = response.data.timestamp
      })
      .catch(e => {
        this.errors.push(e)
      })
  }
}
// async fetch ({ store, params }) {
//  try {
//    let { data } = await axios.get('http://localhost:4000')
//    this.subLines = data.lines
//    store.commit('setMta', data)
//    this.mydata = data
//  } catch (e) {
//    this.errors.push(e)
//  }

//  return {
//    mydata: 33
//  }
// }
</script>

<style>



</style>
