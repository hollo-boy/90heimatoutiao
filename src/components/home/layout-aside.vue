<template>
  <div class="layout-aside">
    <!-- 左侧导航组件 -->
    <el-menu>
      <!-- 没有折叠选项 -->
      <el-menu-item>首页</el-menu-item>
      <!-- 二级折叠菜单 -->
      <el-submenu>
        <template slot="title">
          <span>内容管理</span>
        </template>
        <el-menu-item>发布文章</el-menu-item>
        <el-menu-item>文章列表</el-menu-item>
        <el-menu-item>评论管理</el-menu-item>
        <el-menu-item>素材管理</el-menu-item>

      </el-submenu>
      <el-menu-item>账户信息</el-menu-item>
    </el-menu>
  </div>
</template>

<script>
export default {

}
</script>

<style>

</style>
