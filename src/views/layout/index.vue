<template>
  <el-container>
    <el-aside width="200px">Aside</el-aside>
    <el-container>
      <el-header>Header</el-header>
      <el-main>Main</el-main>
    </el-container>
  </el-container>
</template>

<script>
export default {
  name: 'Layout'
}
</script>

<style lang="scss" scoped>
  .el-container {
    height: 100vh;
    // min-width: 980px;
  }

  .el-aside {
    background-color: #d3dce6;
  }

  .el-header {
    background-color: #b3c0d1;
  }

  .el-main {
    background-color: #e9eef3;
  }
</style>
