<template>
  <el-tree :data="menus" show-checkbox node-key="catId" :props="defaultProps" :expand-on-click-node="false">
     <span class="custom-tree-node" slot-scope="{ node, data }">
        <span>{{ node.label }}</span>
        <span>
          <el-button v-if="node.level <= 2" type="text" size="mini" @click="() => append(data)">
            Append
          </el-button>
          <el-button v-if="node.childNodes.length == 0" type="text" size="mini" @click="() => remove(node, data)">
            Delete
          </el-button>
        </span>
      </span>
  </el-tree>
</template>

<script>
export default {
  name: 'category',
  data () {
    return {
      menus: [],
      defaultProps: {
        children: 'children',
        label: 'name'
      }
    }
  },
  methods: {
    getMenus () {
      this.$http({
        url: this.$http.adornUrl('/product/category/list/tree'),
        method: 'get',
      }).then(({data}) => {
        console.log('数据加载成功', data.data)
        this.menus = data.data
      })
    }
  },
  append (data) {

  },

  remove (node, data) {

  },
  created () {
    this.getMenus()
  }
}
</script>

<style scoped>

</style>
