<template lang="jade">
  code-run-panel
    p {{runRet}}
</template>

<script>
import PubSub from 'pubsub-js'
import axios from 'axios'
import qs from 'qs'

export default {
  data () {
    return {
      runRet: ''
    }
  },
  attached () {
    this.tokens = {
      runCode: PubSub.subscribe('run-code-start', (msg, data) => {
        axios.post('http://code.52zxw.net/test2', qs.stringify({
            code: data,
        }), {headers: {'Content-Type': 'application/x-www-form-urlencoded'}})
        .then((response) => {
          console.log(response.data)
          this.runRet = response.data.stdout
        })
        .catch((error) => {
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
</style>
