<template>
  <div>
    <!--  pc端  -->
    <el-row :gutter="10">
      <el-col :xs="0" :lg="24">
        <div
            style="width: 100%;height: 40px;background-color: #f5f5f5;display: flex;justify-content: space-around;line-height: 40px">
          <div>
            <img style="width: 20px;position: relative;top: 3px" src="@/assets/images/home/wxb.svg" alt="">
            <span style="font-size: 13px">CN <img style="width: 13px;margin: 0 5px" src="@/assets/images/home/next.svg"
                                                  alt=""></span>
            <span style="font-size: 13px">ZH <img style="width: 13px;margin: 0 5px" src="@/assets/images/home/next.svg"
                                                  alt=""></span>
            <span style="font-size: 13px">¥CNY</span>
          </div>
          <div>
            <span style="font-size: 13px">免费国内快递 + 轻松退货</span>
          </div>
          <div style="cursor: pointer">
            <img @click="$router.push('/front/collect')"
                 style="width: 24px;position: relative;top: 5px" src="@/assets/images/home/rebrand-hearts.png"
                 alt="">
            <img @click="$router.push('/front/cart')"
                 style="width: 20px;position: relative;top: 5px;left: 20px" src="@/assets/images/home/bag_1-0.png"
                 alt="">
          </div>
        </div>
      </el-col>
    </el-row>
    <el-row :gutter="10">
      <el-col :xs="0" :lg="24">
        <!--    头部-->
        <div style="width: 100%; height: 60px; line-height: 60px; background-color: white">
          <el-row>
            <el-col :span="3">
              <div style="font-size: 20px; font-weight: bold; text-align: center">
                <img style="width: 20%;margin-right: 10px;position: relative;top: 10px" src="@/assets/images/logo.svg"
                     alt="">
                <a style="color: #409EFF;" href="/front/home">橘子智能</a>
              </div>
            </el-col>
            <el-col :span="12">
              <el-menu class="side-menu" :default-active="$route.path" @select="handleMenuSelect" mode="horizontal">
                <el-menu-item index="/front/home">
                  首页
                </el-menu-item>
                <el-menu-item index="/front/classify">
                  分类
                </el-menu-item>
                <el-menu-item index="/front/cart">
                  购物车
                </el-menu-item>
                <el-menu-item index="/front/order">
                  我的订单
                </el-menu-item>
                <el-menu-item index="/front/collect">
                  收藏夹
                </el-menu-item>
                <el-menu-item index="/front/person">
                  个人中心
                </el-menu-item>
                <el-menu-item index="/front/address">
                  收货地址
                </el-menu-item>
              </el-menu>
            </el-col>
            <el-col :span="6">
              <div v-if="!$route.path.includes('/search')">
                <el-input style="width: 80%" placeholder="请输入商品名称搜索商品" v-model="searchText"></el-input>
                <el-button style="margin-left: 5px" @click="search">搜索</el-button>
              </div>
              <div v-else>
                <div style="width: 100px;height: 20px"></div>
              </div>
            </el-col>
            <el-col :span="3">
              <div style="text-align: right; padding-right: 10px" v-if="user.id">
                <el-dropdown style="float: right;" @command="handleCommand">
              <span class="el-dropdown-link" style="cursor: pointer">
                欢迎你！{{ user.username }}<i class="el-icon-arrow-down el-icon--right"></i>
              </span>
                  <el-dropdown-menu slot="dropdown">
                    <el-dropdown-item command="person">个人信息</el-dropdown-item>
                    <el-dropdown-item command="loginOut">退出登录</el-dropdown-item>
                  </el-dropdown-menu>
                </el-dropdown>
              </div>
              <div style="text-align: right; padding-right: 10px" v-else>
                <el-button @click="$router.replace('/login')">登录</el-button>
                <el-button @click="$router.replace('/register')">注册</el-button>
              </div>

            </el-col>
          </el-row>


        </div>
      </el-col>
    </el-row>
    <el-row :gutter="10">
      <el-col :xs="0" :lg="24">
        <!-- 主体 -->
        <el-row>
          <el-col :span="22" :offset="1" style="margin-bottom: 80px">
            <router-view/>
          </el-col>
        </el-row>
      </el-col>
    </el-row>
    <el-row :gutter="10">
      <el-col :xs="0" :lg="24">
        <Footers/>
      </el-col>
    </el-row>
  </div>
</template>

<script>

import Footers from "./footers";

export default {
  name: "Front",
  components: {
    Footers
  },
  data() {
    return {
      searchText: '',
      user: {}
    }
  },
  created() {
    this.user = sessionStorage.getItem("user") ? JSON.parse(sessionStorage.getItem("user")) : {}
  },
  methods: {
    search() {
      this.$router.replace({path: '/front/search', query: {searchText: this.searchText}})
    },
    handleCommand(command) {
      if (command === 'person') {
        this.$router.push('/front/person');
      }
      if (command === 'loginOut') {
        sessionStorage.removeItem("user")
        this.$router.replace('/login');

      }
    },
    handleMenuSelect(index) {
      console.log(index)
      this.$router.push(index);
    },
  }
}
</script>

<style scoped>

</style>
