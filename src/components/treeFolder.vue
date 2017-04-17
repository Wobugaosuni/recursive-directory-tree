<template>
  <li role="component:treeFolder">
    <div class="list-title">
      <span v-if="isFolder" @click="onOpenIconClick">[{{isOpen ? '-' : '+'}}]</span>
      <span>{{model.name}}</span>
      <span class="file-create-icon" v-if="isFolder" @click="onCreateFileClick">+</span>
    </div>
    <ul v-if="isFolder" v-show="isOpen">
      <tree-folder v-for="childObject in model.children" :model="childObject">
      </tree-folder>
    </ul>
  </li>
</template>

<script type='text/ecmascript-6'>
// import Vue from 'vue'

export default {
  /*
   * 允许组件模板递归地调用自身
   */
  name: 'treeFolder',

  data () {
    return {
      isOpen: true
    }
  },

  props: {
    model: Object
  },

  computed: {
    /*
     * 判断是否有下级目录
     */
    isFolder: function () {
      return this.model.children && this.model.children.length
    }
  },

  methods: {
    onCreateFileClick: function () {
      this.model.children.push({
        'name': 'newIn'
      })
    },

    onOpenIconClick: function () {
      this.isOpen = !this.isOpen
    }
  }
}
</script>

<style lang='stylus' rel='stylesheet/stylus'>
[role="component:treeFolder"]
  .list-title

    .file-create-icon
      color orange
</style>
