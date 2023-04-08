<template>
  <div>
    <el-row :gutter="10">
      <el-col :xs="0" :lg="24">
        <!-- 轮播图 -->
        <swiper/>
      </el-col>
    </el-row>
    <el-row :gutter="10">
      <el-col :xs="0" :lg="24">
        <div style="background-color: #f8f6ed;display: flex;justify-content: space-around">
          <div style="width: 30%;padding-top: 7%;padding-bottom:5%;padding-left: 30px">
            <div style="border-right: 1px solid #d0d0d0">
              <h2 class="home-titles">全场景 智能协同</h2>
              <h2 style="font-size: 20px;color: #353535;margin: 30px 0">再多设备 都能化繁为简</h2>
              <p style="font-size: 16px;margin-bottom: 40px">对话式主动智能</p>
              <div class="home-but" @click="$router.push('/front/classify')">
                <span>更多产品</span>
              </div>
            </div>
          </div>
          <div class="center-img" style="width: 65%;">
            <div @click="goodsDetail(item.id)" v-for="item in recommendList" :key="item.id">
              <img :src="item.imgs[0]" style="width: 25%;float: left; margin: 10px 0; padding-left: 10px;"/>
            </div>
          </div>
        </div>
      </el-col>
    </el-row>
    <el-row :gutter="10">
      <el-col :xs="0" :lg="24">
        <div style="font-size: 18px;line-height: 22px;">
          <div style="width: 100%;text-align: center;position: relative;top: 20px">
            <h4 class="main-titles" style="padding: 30px 0 0 0;font-size: 20px">定制化情感声音</h4>
            <h3 class="home-titles" style="padding: 10px 0 30px 0;font-size: 30px">
              更主动的对话式服务，更加个人的专属体验!</h3>
          </div>
        </div>
      </el-col>
    </el-row>
    <el-row :gutter="10">
      <el-col :xs="0" :lg="24">
        <div style="margin-top: 10px">
          <el-row :gutter="10">
            <!--    推荐商品-->
            <el-col :span="18">
              <el-card>
                <div style="padding: 10px 0; border-bottom: 2px solid #0ce751; font-size: 20px; color: #2de130">
                  热门商品
                </div>
                <div style="padding: 10px 0">
                  <el-row :gutter="10">
                    <el-col :span="6" v-for="item in goodsList" :key="item.id" style="margin-bottom: 10px">
                      <div class="home-goods" @click="goodsDetail(item.id)">
                        <el-image :src="item.imgs[0]" class="home-goods-img" style="width: 100%; height: 100px"
                                  fit="contain"></el-image>
                        <div style="padding: 5px; height: 20px; text-align: center; font-size: 12px; overflow: hidden">
                          <el-tooltip :content="item.name" placement="bottom" effect="light">
                            <span class="item-title">{{ item.name }}</span>
                          </el-tooltip>
                        </div>
                        <div style="padding: 5px; text-align: center; color: red; font-size: 12px">
                          ￥ {{ item.price }}
                        </div>
                      </div>

                    </el-col>
                  </el-row>
                </div>
              </el-card>
              <el-card style="margin-top:2%">
                <div style="padding: 10px 0; border-bottom: 2px solid orangered; font-size: 20px; color: orangered">
                  推荐商品
                </div>
                <div style="padding: 10px 0">
                  <el-row :gutter="10">
                    <el-col :span="6" v-for="item in recommend" :key="item.id" style="margin-bottom: 10px">
                      <div class="home-goods" @click="goodsDetail(item.id)">
                        <el-image :src="item.imgs[0]" class="home-goods-img" style="width: 100%; height: 100px"
                                  fit="contain"></el-image>
                        <div style="padding: 5px; height: 20px; text-align: center; font-size: 12px; overflow: hidden">
                          <el-tooltip :content="item.name" placement="bottom" effect="light">
                            <span class="item-title">{{ item.name }}</span>
                          </el-tooltip>
                        </div>
                        <div style="padding: 5px; text-align: center; color: red; font-size: 12px">
                          ￥ {{ item.price }}
                        </div>
                      </div>
                    </el-col>
                  </el-row>
                </div>
              </el-card>
            </el-col>
            <!--        销售排行-->
            <el-col :span="6">
              <el-card>
                <div style="padding: 10px 0; border-bottom: 2px solid dodgerblue; font-size: 20px; color: dodgerblue">
                  销量排行榜
                </div>

                <div style="padding: 10px 0">
                  <el-row v-for="(item, index) in sales" :key="item.id">
                    <div style="padding: 10px 0; cursor: pointer;" @click="goodsDetail(item.id)">
                      <el-col :span="2" style="padding-top: 5px">
                        <span v-if="index === 0" style="color: gold">{{ index + 1 }}</span>
                        <span v-if="index === 1" style="color: silver">{{ index + 1 }}</span>
                        <span v-if="index === 2" style="color: coral">{{ index + 1 }}</span>
                        <span v-if="index > 2">{{ index + 1 }}</span>
                      </el-col>
                      <el-col :span="10">
                        <el-image class="home-goods-img" :src="item.imgs[0]" style="width: 100%; height: 80px"
                                  fit="contain"></el-image>
                      </el-col>
                      <el-col :span="12">
                        <div style="overflow: hidden; height: 80px; font-size: 12px">
                          {{ item.description }}
                        </div>
                      </el-col>
                    </div>
                  </el-row>
                </div>
              </el-card>
            </el-col>
          </el-row>
        </div>
      </el-col>
    </el-row>
    <el-row :gutter="10">
      <el-col :xs="0" :lg="24">
        <div style="margin: 30px 0 30px 0;">
          <img style="width: 100%;border-radius: 10px" src="@/assets/images/home/footer05.png" alt="">
        </div>
      </el-col>
    </el-row>
    <el-row :gutter="10">
      <el-col :xs="0" :lg="24">
        <div style="display: flex;justify-content: space-between;margin: 10px auto 50px;">
          <img style="border-radius: 25px" src="@/assets/images/home/footer02.jpg" alt="">
          <img style="border-radius: 25px" src="@/assets/images/home/footer03.jpg" alt="">
          <img style="border-radius: 25px" src="@/assets/images/home/footer04.jpg" alt="">
        </div>
      </el-col>
    </el-row>
  </div>
</template>

<script>
import API from "@/utils/request";
import swiper from "../../components/common/swiper";

const url = "/api/video/"

export default {
  name: "Home",
  components: {
    swiper
  },
  data() {
    return {
      sales: [],
      recommend: [],
      recommendList: [],
      goodsList: [],
      user: {},
    };
  },
  created() {
    this.user = sessionStorage.getItem("user") ? JSON.parse(sessionStorage.getItem("user")) : {}
    this.load()
  },
  methods: {
    goodsDetail(id) {
      this.$router.replace({path: '/front/goods', query: {id: id}})
    },
    load() {
      API.get("/api/goods/recommend").then(res => {
        this.recommend = res.data.splice(0, 8)
        this.recommend.forEach(item => {
          // 处理下表格的图片显示
          if (!item.imgs) {
            item.imgs = ['']
          } else {
            item.imgs = JSON.parse(item.imgs)
          }
        })
      })
      API.get("/api/goods/sales").then(res => {
        this.sales = res.data.splice(0, 10)
        this.sales.forEach(item => {
          // 处理下表格的图片显示
          if (!item.imgs) {
            item.imgs = ['']
          } else {
            item.imgs = JSON.parse(item.imgs)
          }
        })
      })

      API.get("api/goods").then(res => {
        this.goodsList = res.data.splice(0, 8)
        this.recommendList = res.data.splice(15, 8)
        console.log(this.recommendList)

        this.recommendList.forEach(item => {
          // 处理下表格的图片显示
          if (!item.imgs) {
            item.imgs = ['']
          } else {
            item.imgs = JSON.parse(item.imgs)
          }
        })
        this.goodsList.forEach(item => {
          // 处理表格图片
          if (!item.imgs) {
            item.imgs = ['']
          } else {
            item.imgs = JSON.parse(item.imgs)
          }
        })
      })

    },
  },
};
</script>

<style lang="less" scoped>
.home-titles {
  background-image: linear-gradient(92.03deg, #15cefe 13.82%, #d080d4 87.25%);
  color: transparent;
  -webkit-background-clip: text;
  font-size: 40px;
  font-weight: bold
}

.home-but {
  background-color: #cab380;
  color: #fff;
  font-size: 13px;
  width: 160px;
  height: 35px;
  text-align: center;
  line-height: 35px;
  cursor: pointer;
}

.home-but:hover {
  background-color: #ec6f15;
}

.center-img img {
  width: 10%;

}

.center-img img:hover,
.tui-img:hover {
  transition: all .3s linear;
  transform: translate3d(0, -2px, 0);
}

.center-item {
  display: flex;
  width: 100%;
}

.center-item img {
  cursor: pointer;
}


.main-titles::before {
  position: absolute;
  content: "";
  top: 0;
  left: 0;
  right: 0;
  width: 10%;
  height: 3px;
  margin-left: auto;
  margin-right: auto;
  background-color: #ba2327;
  z-index: 1;
}

.main-titles:hover {
  color: #4a4a4a;
}


.item-title {
  cursor: pointer;
}

.item-title:hover {
  color: orangered;
}

.home-goods {
  border: 1px solid #ccc;
  cursor: pointer;
  padding: 20px;
}

.home-goods-img:hover,
.home-goods:hover {
  transition: all .3s linear;
  box-shadow: 0 15px 30px rgb(0 0 0 / 10%);
  transform: translate3d(0, -2px, 0);
}
</style>
