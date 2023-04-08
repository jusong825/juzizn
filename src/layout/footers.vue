<template>
<div>
  <!--  pc端  -->
  <el-row :gutter="10">
    <el-col :xs="0" :lg="24">
      <div class="footer">
        <span>2022 © 橘子.智能</span>
        <a href="https://beian.miit.gov.cn/" target="_blank" style="
      text-decoration: none;margin-left: 30px;font-size: 16px;color: #fff">湘ICP备8798761645号-1
        </a>
      </div>
    </el-col>
  </el-row>
</div>
</template>

<script>
export default {
  name: "footers"
}
</script>

<style scoped>
.footer {
  text-align: center;
  width: 100%;
  height: 170px;
  line-height: 170px;
  color: #fff;
  background: url(../assets/images/home/footer-new.jpeg) no-repeat 0 -18px #013529;
  background-size: cover
}
</style>
