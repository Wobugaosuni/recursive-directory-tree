<template>
  <li role="component:treeFolder">
    <div class="list-title">
      <span v-if="isFolder" @click="onOpenIconClick">[{{isOpen ? '-' : '+'}}]</span>
      <span @dblclick="changeToDirectory">{{model.name}}</span>
      <span class="file-create-icon" v-if="isFolder" @click="onCreateFileClick">+</span>
    </div>
    <ul v-if="isFolder" v-show="isOpen">
      <tree-folder v-for="childObject in model.children" :model="childObject">
      </tree-folder>
    </ul>
  </li>
</template>

<script type='text/ecmascript-6'>
import Vue from 'vue'

export default {
  /*
   * 允许组件模板递归地调用自身
   */
  name: 'treeFolder',

  data () {
    return {
      isOpen: false
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
    changeToDirectory: function () {
      if (!this.isFolder) {
        Vue.set(this.model, 'children', [])
        this.isOpen = true
        this.onCreateFileClick()
      }
    },

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
      display inline-block
      padding 0 15px
      color blue
</style>
