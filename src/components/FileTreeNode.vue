<template>
  <ul :class="['item', {'directory': isDirectory, 'file': isFile, 'link': isLink, 'open': isOpened && isFolder}]">
    <li @click.prevent.stop="toggle">
      <div :class="{'selected': isSelected}">{{ item.name }}</div>
      <ul v-if="isOpened && isFolder">
        <file-tree-node :path="`${path}/${item.name}`" :selected-path="selectedPath"
                        v-for="(child, index) in item.contents" :key="index" :item="child" @select="select"/>
      </ul>
    </li>
  </ul>
</template>

<script>
export default {
  name: "FileTreeNode",
  props: {
    path: {
      type: String,
      default: ""
    },
    selectedPath: {
      type: String,
      default: undefined
    },
    item: Object
  },
  data: () => {
    return {
      isOpened: false,
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
    },
    isSelected: function () {
      return `${this.path}/${this.item.name}` === this.selectedPath;
    }
  },
  methods: {
    toggle: function () {
      if (this.isFolder) {
        this.isOpened = !this.isOpened;
        if (this.selectedPath && this.selectedPath.startsWith(`${this.path}/${this.item.name}`)) {
          this.$emit("select", undefined);
        }
      } else if (this.isLink || this.isFile) {
        this.$emit("select", `${this.path}/${this.item.name}`);
      }
    },
    select: function (path) {
      this.$emit("select", path);
    }
  },
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