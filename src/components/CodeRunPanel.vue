<template lang="jade">
  code-run-panel
    h1 {{hello}}
</template>

<script>
import PubSub from 'pubsub-js'
import axios from 'axios'
import qs from 'qs'

export default {
  data () {
    return {
      hello: 'Hello World!'
    }
  },
  attached () {
    this.tokens = {
      runCode: PubSub.subscribe('run-code-start', (msg, data) => {
        // console.log('123')
        this.hello = 'Hello, My World'
        axios.post('http://code.52zxw.net/test2', qs.stringify({
            code: data,
        }), {headers: {'Content-Type': 'application/x-www-form-urlencoded'}})
        .then(function (response) {
          console.log(response.data)
        })
        .catch(function (error) {
          console.log(error)
        })
      })
    }
  },
  destroyed () {
    for (let key in this.tokens) {
      PubSub.unsubscribe(this.tokens[key])
    }
  }
}
</script>

<style lang="stylus" scoped>
  code-run-panel
    flex: 0 0 auto
    height: 30%
  h1
    color: red
</style>
