<template>
  <!--    分类 -->
  <div style="margin-top: 10px">
    <el-card>
      <el-row :gutter="10">
        <!--          分类-->
        <el-col :span="4">
          <div style=" text-align: center; border-bottom: none;box-shadow: 0 15px 30px rgb(0 0 0 / 10%);">
            <div class="category-item" @click="getGoodsByCategory(item.id)" v-for="item in categories" :key="item.id"
                 :class="{ active: (activeIndex === item.id)}">{{ item.name }}
            </div>
          </div>
        </el-col>

        <el-col :span="20">
          <!--          分类商品-->
          <div style="min-height: 150px">
            <el-row :gutter="10">
              <el-col :span="6" v-for="item in tableData" :key="item.id">
                <div style="margin-bottom: 10px; cursor: pointer" @click="goodsDetail(item.id)">
                  <div style="padding: 5px">
                    <el-image :src="item.imgs[0]" style="width: 100%; height: 100px" fit="contain"></el-image>
                  </div>
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

          <!--      分页-->
          <div style="margin-top: 20px">
            <el-pagination
                small
                @size-change="handleSizeChange"
                @current-change="handleCurrentChange"
                :current-page="pageNum"
                :page-size="pageSize"
                :page-sizes="[4, 8, 12]"
                layout=" prev, pager, next"
                :total="total"
            >
            </el-pagination>
          </div>

        </el-col>
      </el-row>
    </el-card>

  </div>
</template>

<script>
import API from "../../utils/request";

export default {
  name: "classify",
  data() {
    return {
      tableData: [],
      activeIndex: 0,
      categories: [],
      pageNum: 1,
      pageSize: 8,
      total: 0
    };
  },
  created() {
    this.load()
  },
  methods: {
    goodsDetail(id) {
      this.$router.replace({path: '/front/goods', query: {id: id}})
    },
    getGoodsByCategory(id) {
      this.activeIndex = id
      this.loadTable(id)
    },
    load() {
      API.get("/api/category").then(res => {
        this.categories = res.data
        this.activeIndex = res.data[0].id
        this.loadTable(res.data[0].id)
      })
    },
    loadTable(categoryId) {
      API.get("/api/goods/byCategory/" + categoryId, {
        params: {
          pageNum: this.pageNum,
          pageSize: this.pageSize
        }
      }).then(res => {
        this.tableData = res.data.records
        this.total = res.data.total

        this.tableData.forEach(item => {
          // 处理下表格的图片显示
          if (!item.imgs) {
            item.imgs = ['']
          } else {
            item.imgs = JSON.parse(item.imgs)
          }
        })
      })
    },
    handleSizeChange(pageSize) {
      this.pageSize = pageSize;
      this.loadTable(this.categories[0].id)
    },
    handleCurrentChange(pageNum) {
      this.pageNum = pageNum;
      this.loadTable(this.categories[0].id)
    }
  },
}
</script>

<style scoped>
.item-title {
  cursor: pointer;
}

.item-title:hover {
  color: orangered;
}

.active {
  color: #127dcb !important;
}

.category-item {
  padding: 7px 0;
  color: #666;
  cursor: pointer;
}
</style>
