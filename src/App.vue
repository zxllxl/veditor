<template lang="jade">
  app#app
    menu-bar
    main-panel
      side-bar
        open-file-panel
        file-panel
      resize-bar
      editor-panel
    code-run-panel
</template>

<script>
import MenuBar from './components/MenuBar'
import OpenFilePanel from './components/OpenFilePanel'
import FilePanel from './components/FilePanel'
import EditorPanel from './components/EditorPanel'
import ResizeBar from './components/ResizeBar'
import CodeRunPanel from './components/CodeRunPanel'

export default {
  components: {
    MenuBar,
    OpenFilePanel,
    FilePanel,
    EditorPanel,
    ResizeBar,
    CodeRunPanel
  }
}
</script>

<style lang="less">
@import "./less/index.less";
</style>
