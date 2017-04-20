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
     <div class="create-new-wrapper" v-if="createNew">
      <input
        type="text"
        class="create-new"
        placeholder="请输入"
        v-focus="createNew"
        v-model.trim="selfDefinedModelName"
        @change="onNameInputFinished"
        @blur="onNameInputBlur" />
    </div>
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
      isOpen: false,
      createNew: false,
      selfDefinedModelName: ''
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
      return this.model.children
      // return this.model.children && this.model.children.length
    }
  },

  // beforeCreate: function () {
  //   this.$options.components.tagTreeFolderContent = require('../tagTreeFolderContent/tagTreeFolderContent')
  // },

  directives: {
    focus: {
      inserted: function (el, {value}) {
        if (value) {
          // console.log('el', el);
          el.focus()
        }
      }
    }
  },

  methods: {
    changeToDirectory: function () {
      if (!this.isFolder) {
        Vue.set(this.model, 'children', [])
        this.isOpen = true
        // console.log('this.model', this.model)
        // console.log('this.open', this.isOpen)
        // this.onCreateFileClick()
      }
    },

    onCreateFileClick: function () {
      this.isOpen = true
      this.createNew = true
      // this.model.children.push({
      //   'name': 'newIn'
      // })
    },

    onNameInputFinished: function () {
      if (this.selfDefinedModelName) {
        this.model.children.push({
          name: this.selfDefinedModelName
          // children: []
        })
      }
      this.selfDefinedModelName = ''
      this.createNew = false
    },

    onNameInputBlur: function () {
      this.createNew = false
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

  .create-new-wrapper
    font-size 12px
    margin 6px 0 0 20px

    .create-new
      display inline-block
      padding 3px 6px
</style>
