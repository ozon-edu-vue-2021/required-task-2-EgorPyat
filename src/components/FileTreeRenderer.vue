<template>
  <ul :class="['item', {'directory': isDirectory, 'file': isFile, 'link': isLink, 'open': isOpened && isFolder}]">
    <li>
      <div @click="toggle" :class="{'selected': isSelected}">{{ item.name }}</div>
      <ul v-if="isOpened && isFolder">
        <file-tree-renderer v-for="(child, index) in item.contents" :key="index" :item="child"/>
      </ul>
    </li>
  </ul>
</template>

<script>
export default {
  name: "FileTreeRenderer",
  props: {
    item: Object
  },
  data: () => {
    return {
      isOpened: false,
      isSelected: false,
    };
  },
  computed: {
    isFolder: function () {
      return this.item.contents && this.item.contents.length;
    },
    isDirectory: function () {
      return this.item.type === "directory";
    },
    isFile: function () {
      return this.item.type === "file";
    },
    isLink: function () {
      return this.item.type === "link";
    }
  },
  methods: {
    toggle: function () {
      if (this.isFolder) {
        this.isOpened = !this.isOpened;
      }
      this.isSelected = !this.isSelected;
    }
  }
}
</script>

<style scoped>
.item {
  cursor: pointer;
}

.directory {
  color: red;
  list-style-type: disclosure-closed;
}

.directory.open {
  color: red;
  list-style-type: disclosure-open;
}

.file {
  color: green;
  list-style-type: ethiopic-numeric;
}

.link {
  color: blue;
  list-style-type: cambodian;
}

.selected {
  font-weight: bold;
}

ul {
  padding-left: 1em;
  line-height: 1.5em;
}
</style>