<template>
    <el-tree :data="data" :props="defaultProps" @node-click="handleNodeClick" />
</template>

<script>
  export default {
    data() {
      return {
        data: [],
        defaultProps: {
          children: 'children',
          label: 'label'
        }
      };
    },
    methods: {
      handleNodeClick(data) {
        console.log(data);
      },
      getDataList () {
        this.dataListLoading = true
        this.$http({
          url: this.$http.adornUrl('/product/category/list/tree'),
          method: 'get'
        }).then(({data}) => {
          if (data && data.code === 0) {
            this.data = data.categorys
          }
          this.dataListLoading = false
        })
      }
    },
    created() {
      this.getDataList();
    }
  };
</script>

<style>
</style>
