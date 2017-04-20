<template>
  <tree-folder :model="model"></tree-folder>
</template>

<script>
  import treeFolder from '../treeFolder/treeFolder.vue';
  export default {
    props: {
      model: Object
    },

    components: {
      'tree-folder': treeFolder
    }
  };
</script>
