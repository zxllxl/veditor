<template lang="jade">
  code-run-panel
    textarea {{runRet}}
</template>

<script>
import PubSub from 'pubsub-js'
import axios from 'axios'
import qs from 'qs'

export default {
  data () {
    return {
      lang: 'text',
      runRet: ''
    }
  },
  attached () {
    this.tokens = {
      codeLang: PubSub.subscribe('code-lang', (msg, data) => {
        this.lang = data
        console.log('CodeRunPanel:22:'+data)
      }),
      runCode: PubSub.subscribe('run-code-start', (msg, data) => {
        this.runRet = 'running...'
        axios.post('http://code.52zxw.net/test2', qs.stringify({
          lang: this.lang,
          code: data,
        }), {headers: {'Content-Type': 'application/x-www-form-urlencoded'}})
        .then((response) => {
          console.log(response.data)
          var runRet = ''
          if (response.data.stderr != '') {
            runRet = response.data.stderr
          } else {
            runRet = response.data.stdout
          }
          this.runRet = runRet
        })
        .catch((error) => {
          console.log(error)
          this.runRet = 'error!'
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
    textarea
      width: 100%
      height: 100%
      padding: 10px
</style>
