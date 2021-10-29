<template>
  <file-tree-node path="" :item="nodes" :selected-path="selectedPath" @select="select"/>
</template>

<script>
import FileTreeNode from "../components/FileTreeNode";

export default {
  name: "FileTreeRenderer",
  components: {
    FileTreeNode
  },
  props: {
    nodes: Object
  },
  data: () => {
    return {
      selectedPath: undefined,
    };
  },
  methods: {
    select: function (path) {
      this.selectedPath = path
    }
  },
}
</script>

<style scoped>

</style>