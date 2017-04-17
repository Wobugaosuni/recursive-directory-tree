<template>
  <div id='app'>
    <ul>
      <tree-folder
        :model='myTree'>
      </tree-folder>
    </ul>
  </div>
</template>

<script>
import treeFolder from './components/treeFolder'
// import axios from 'axios'

export default {
  name: 'app',

  data () {
    return {
      myTree: {
        'name': 'My Tree',
        'children': [
          { 'name': 'hello' },
          { 'name': 'son' },
          {
            'name': 'child folder',
            'children': [
              {
                'name': 'child child folder1',
                'children': [
                  { 'name': 'child child hello1' },
                  { 'name': 'child child son1' }
                ]
              },
              { 'name': 'child hello' },
              { 'name': 'child son' },
              {
                'name': 'child child folder2',
                'children': [
                  { 'name': 'child child hello2' },
                  { 'name': 'child child son2' }
                ]
              }
            ]
          }
        ]
      }
    }
  },

  components: {
    treeFolder
  },

  created () {
    // axios.get('/api/my-tree').then((response) => {
    //   this.myTree = response.data.data
    //   console.log('myTree', this.myTree)
    // })
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  /*text-align: center;*/
  color: #2c3e50;
  margin-top: 30px;
}
</style>
