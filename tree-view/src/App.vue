<template>
  <ul id="app">
    <TreeItem :model="treeData"></TreeItem>
  </ul>
</template>

<script>
import TreeItem from "./TreeItem.vue";
export default {
  name: "app",
  components: {
     TreeItem
  },
  data: function() {
    return {
      treeData: {
        name: "My Tree",
        children: [
          { name: "hello" },
          { name: "wat" },
          {
            name: "child folder",
            children: [
              {
                name: "child folder",
                children: [{ name: "hello" }, { name: "wat" }]
              },
              { name: "hello" },
              { name: "wat" },
              {
                name: "child folder",
                children: [{ name: "hello" }, { name: "wat" }]
              }
            ]
          }
        ]
      }
    };
  }
};
</script>

<style>
</style>
