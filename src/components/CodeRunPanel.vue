<template lang="jade">
  code-run-panel
    h1 {{hello}}
</template>

<script>
export default {
  data () {
    return {
      hello: 'Hello World!'
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
