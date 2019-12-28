<template>
       <el-carousel :interval="5000" arrow="always"  type="card" height="200px">
    <el-carousel-item v-for="item in list" :key="item">
      <img :src="item" alt="" width="100%">
    </el-carousel-item>
  </el-carousel>
</template>

<script>
export default {
  data () {
    return {
      list: ['http://img2.imgtn.bdimg.com/it/u=1968765211,2786040509&fm=26&gp=0.jpg', 'http://attachments.gfan.com/forum/attachments2/day_100622/100622225201fe0a288cbb569f.jpg', 'http://file.mumayi.com/forum/201401/16/202014h22z6jt6vpajypd0.jpg']
    }
  }
}
</script>

<style>
  .el-carousel__item:nth-child(2n) {
    background-color: #99a9bf;
  }

  .el-carousel__item:nth-child(2n+1) {
    background-color: #d3dce6;
  }
</style>
