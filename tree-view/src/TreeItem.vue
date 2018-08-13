<template>
<li>
  <div :class="{bold: isFolder}"
  @click="toggle"
  @dblclick="changeType"
  >
    {{model.name}}
    <span v-show="isFolder">[{{this.open?'-':'+'}}]</span>
  </div>
  <ul v-show="open">
    <TreeItem 
    v-for="(child,index) in model.children"
    :key="index"
    :model="child"
    >
    </TreeItem>
    <li @click="addChild">+</li>
  </ul>
</li>
</template>

<script>
import Vue from 'vue'
export default {
  name: 'TreeItem',
  props: {
    model: Object
  },
  data: function () {
    return {
      open: false
    }
  },
  computed: {
    isFolder: function () {
      return this.model.children && this.model.children.length
    }
  },
  methods: {
    toggle: function () {
      if (this.isFolder) {
        this.open = !this.open
      }
    },
    addChild: function () {
      this.model.children.push({name:'new stuff'})
    },
    changeType: function () {
      if (this.isFolder) return
      Vue.set(this.model, 'children', [])  
      this.addChild()
      this.open = true
    }
  }
}
</script>

<style>
.bold {
  font-weight: bold;
}
</style>
