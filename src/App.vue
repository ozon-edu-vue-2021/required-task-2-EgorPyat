<template>
  <div id="app">
    <file-tree-renderer :nodes="nodes"/>
  </div>
</template>

<script>
import FileTreeRenderer from "./components/FileTreeRenderer";
import nodes from "../public/static/node_modules.json";

export default {
  name: 'App',
  components: {
    FileTreeRenderer
  },
  data: () => ({
    nodes: nodes
  })
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
}
</style>
