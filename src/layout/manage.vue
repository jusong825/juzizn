<template>
  <div>
    <!--  pc端  -->
    <el-row :gutter="10">
      <el-col :xs="0" :lg="24">
        <div class="app-container">
          <header>
            <img style="width: 2%;position: relative;top: 7px" src="@/assets/images/logo.svg" alt="">
            橘子智能
            <el-dropdown style="float: right;" @command="handleCommand">
        <span class="el-dropdown-link" style="cursor: pointer;color: #fff">
          欢迎你！{{ user.username }}<i class="el-icon-arrow-down el-icon--right"></i>
        </span>
              <el-dropdown-menu slot="dropdown">
                <el-dropdown-item command="person">个人信息</el-dropdown-item>
                <el-dropdown-item command="loginOut">退出登录</el-dropdown-item>
              </el-dropdown-menu>
            </el-dropdown>
          </header>
          <div class="main-content">
            <el-menu class="side-menu" :default-active="$route.path" @select="handleMenuSelect"
                     background-color="#545c64" text-color="#fff" active-text-color="#409EFF">
              <el-menu-item :index="item.path" v-for="item in user.permission" :key="item.path">
                <template slot="title">
                  <i :class="['el-icon-' + item.icon]"></i>
                  <span>{{ item.name }}</span>
                </template>
              </el-menu-item>
            </el-menu>

            <router-view class="main-container" :key="Math.random()" @call="getMenu"/>
          </div>
        </div>
      </el-col>
    </el-row>
  </div>
</template>

<script>


export default {
  name: 'Manage',
  components: {},
  data() {
    return {
      user: {},
      permissions: []
    };
  },
  created() {
    this.getMenu()
  },
  methods: {
    getMenu() {
      this.user = sessionStorage.getItem("user") ? JSON.parse(sessionStorage.getItem("user")) : {}
      this.user.permission.forEach(item => {
        item.path = "/manage" + item.path
      })
    },
    handleCommand(command) {
      if (command === 'person') {
        this.$router.push('/manage/person');
      }
      if (command === 'loginOut') {
        sessionStorage.removeItem("user")
        this.$router.replace('/login');

      }
    },
    handleMenuSelect(index) {
      console.log(this.$router.getRoutes())
      this.$router.push(index);
    },
  },
  computed: {},
}
</script>

<style scoped>
.app-container {
  display: flex;
  flex-direction: column;
  height: 100%;
}

header {
  margin-bottom: 3px;
  line-height: 50px;
  padding: 0 16px;
  font-size: 18px;
  font-weight: bold;
  color: #fff;
  background-color: #545c64;
  box-shadow: 0 0 4px 4px #e6e6e6;
}

.main-content {
  flex: 1;
  display: flex;
  flex-direction: row;
}

.main-container {
  margin-left: 3px;
  padding: 10px;
  flex: 1;
  overflow-y: auto;
  background-color: #fff;
}

.side-menu {
  width: 200px;
  height: 100%;

}

.el-menu-item a {
  text-decoration: none;
}

.el-menu-item.is-active a {
  color: #409EFF;
}
</style>
