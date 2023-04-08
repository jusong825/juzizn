<template>
  <div>
    <!--  pc端  -->
    <el-row :gutter="10">
      <el-col :xs="0" :lg="24">
        <div style="margin-top: 10px">
          <el-carousel height="400px" :interval="4000" type="card">
            <el-carousel-item v-for="item in imgList" :key="item.id">
              <a target="_blank" :href="item.url">
                <img style="width: 100%;height: 400px;border-radius: 10px" :src='item.img' alt="">
              </a>
            </el-carousel-item>
          </el-carousel>
        </div>
      </el-col>
    </el-row>
  </div>
</template>

<script>
import API from "../../utils/request";

export default {
  name: "swiper",
  data() {
    return {
      imgList: []
    }
  },
  mounted() {
    this.load();
  },
  methods: {
    load() {
      API.get("/api/banner").then(res => {
        this.imgList = res.data
      })
    },
    goodsDetail(id) {
      this.$router.replace({path: '/front/goods', query: {id: id}})
    },
  }
}
</script>

<style scoped>

</style>
