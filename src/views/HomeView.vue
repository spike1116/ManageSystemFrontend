<template>
  <el-container style="min-height: 100vh;">
    <el-aside :width="siedeWidth+'px'"
      style="background-color: rgb(238, 241, 246); box-shadow: 2px 0 6px rgb(0 21 41 /35%)">
      <el-menu :default-openeds="['1', '3']" style="min-height: 100%;overflow-x: hidden"
        background-color="rgb(48,65,86)" text-color="#fff" active-text-color="#ffd04b" :collapse-transition="false"
        :collapse="isCollapse">
        <div style="height: 60px; line-height: 60px; text-align: center;">
          <img src="../assets/logo.png" alt="" style="width: 20px; position:relative;top: 5px;margin-right: 5px;">
          <b style="color:white" v-show="logTextShow">后台管理系统</b>

        </div>
        <el-submenu index="1">
          <template slot="title"><i class="el-icon-message"></i>
            <span slot="title">导航一</span>
          </template>
          <el-menu-item-group>
            <template slot="title">分组一</template>
            <el-menu-item index="1-1">选项1</el-menu-item>
            <el-menu-item index="1-2">选项2</el-menu-item>
          </el-menu-item-group>
          <el-menu-item-group title="分组2">
            <el-menu-item index="1-3">选项3</el-menu-item>
          </el-menu-item-group>
          <el-submenu index="1-4">
            <template slot="title">选项4</template>
            <el-menu-item index="1-4-1">选项4-1</el-menu-item>
          </el-submenu>
        </el-submenu>
        <el-submenu index="2">
          <template slot="title"><i class="el-icon-menu"></i>
            <span slot="title">导航一</span>
          </template>
          <el-menu-item-group>
            <template slot="title">分组一</template>
            <el-menu-item index="2-1">选项1</el-menu-item>
            <el-menu-item index="2-2">选项2</el-menu-item>
          </el-menu-item-group>
          <el-menu-item-group title="分组2">
            <el-menu-item index="2-3">选项3</el-menu-item>
          </el-menu-item-group>
          <el-submenu index="2-4">
            <template slot="title">选项4</template>
            <el-menu-item index="2-4-1">选项4-1</el-menu-item>
          </el-submenu>
        </el-submenu>
        <el-submenu index="3">
          <template slot="title"><i class="el-icon-setting"></i>
            <span slot="title">导航一</span>
          </template>
          <el-menu-item-group>
            <template slot="title">分组一</template>
            <el-menu-item index="3-1">选项1</el-menu-item>
            <el-menu-item index="3-2">选项2</el-menu-item>
          </el-menu-item-group>
          <el-menu-item-group title="分组2">
            <el-menu-item index="3-3">选项3</el-menu-item>
          </el-menu-item-group>
          <el-submenu index="3-4">
            <template slot="title">选项4</template>
            <el-menu-item index="3-4-1">选项4-1</el-menu-item>
          </el-submenu>
        </el-submenu>
      </el-menu>
    </el-aside>

    <el-container>
      <el-header style="font-size: 12px;border-bottom:1px solid;line-height: 60px; display:flex">
        <div style="flex:1;font-size: 18px;">
          <span :class="collapseBtnClass" style="cursor:pointer;width: 20px;" @click="collapse"></span>
        </div>
        <el-dropdown style="width: 80px; cursor: pointer;">
          <span>Settings</span><i class="el-icon-arrow-down" style="margin: 5px;"></i>
          <el-dropdown-menu slot="dropdown">
            <el-dropdown-item>个人信息</el-dropdown-item>
            <el-dropdown-item>退出</el-dropdown-item>
          </el-dropdown-menu>
        </el-dropdown>
      </el-header>

      <el-main>
        <div style="margin: 10px 0;">
          <el-input style="width: 200px" suffix-icon="el-icon-search" placeholder="请输入查询内容"
            v-model="bookName"></el-input>
          <el-button class="ml-5" type="primary" @click="load()">搜索</el-button>
        </div>
        <div style="margin:10px 0;">
          <el-button type="primary">新增 <i class="el-icon-circle-plus-outline"></i></el-button>
          <el-button type="danger">批量删除 <i class="el-icon-remove-outline"></i></el-button>
          <el-button type="primary">导入 <i class="el-icon-bottom"></i></el-button>
          <el-button type="primary">导出 <i class="el-icon-top"></i></el-button>
        </div>
        <el-table :data="tableData" stripe :header-cell-class-name="headerBg">
          <el-table-column prop="id" label="Id" width="140" hidden="true">
          </el-table-column>
          <el-table-column prop="book_name" label="书名" width="140">
          </el-table-column>
          <el-table-column prop="book_author" label="作者" width="120">
          </el-table-column>
          <el-table-column prop="book_category" label="类型" width="120">
          </el-table-column>
          <el-table-column prop="book_publisher" label="出版社" width="120">
          </el-table-column>
          <el-table-column label="操作">
            <template slot-scope="scope">
              <el-button type="success">编辑 <i class="el-icon-edit"></i></el-button>
              <el-button type="danger">删除 <i class="el-icon-delete"></i></el-button>
            </template>
          </el-table-column>
        </el-table>
        <div style="padding: 10px 0;">
          <el-pagination @size-change="handleSizeChange" @current-change="handleCurrentChange" :current-page="pageNum"
            :page-sizes="[2, 5, 10, 20]" :page-size="pageSize" layout="total, sizes, prev, pager, next, jumper"
            :total="total">
          </el-pagination>
        </div>
      </el-main>
    </el-container>
  </el-container>
</template>


<style>
  .el-header {
    color: #B3C0D1;

    line-height: 60px;
  }

  .el-aside {
    color: #333;
    transition: width 0.25s;
    -webkit-transition: width 0.25s;
    -moz-transition: width 0.25s;
    -webkit-transition: width 0.25s;
    -o-transition: width 0.25s;
  }

  .headerHg {
    background: #eee !important;
  }
</style>

<script>
  export default {
    data () {
      return {
        tableData: [],
        total: 0,
        pageNum: 1,
        pageSize: 2,
        collapseBtnClass: "el-icon-s-fold",
        isCollapse: false,
        siedeWidth: 200,
        logTextShow: true,
        headerBg: 'headerBg',
        bookName: ""
      }
    },
    created () {
      // 请求分页查询数据
      this.load()
    },
    devServer: {
      proxy: {
        '/book': {
          target: 'http://localhost:9091',
          changeOrigin: true
        }
      }
    },
    methods: {
      collapse () {
        this.isCollapse = !this.isCollapse
        this.logTextShow = !this.logTextShow
        if (this.isCollapse) {
          this.siedeWidth = 64
          this.collapseBtnClass = 'el-icon-s-unfold'
        } else {
          this.siedeWidth = 200
          this.collapseBtnClass = 'el-icon-s-fold'
        }
        console.log("Triggered")
      },
      handleSizeChange (pageSize) {
        console.log(`每页 ${pageSize} 条`)
        this.pageSize = pageSize
        this.load()
      },
      handleCurrentChange (pageNum) {
        console.log(`当前页: ${pageNum}`)
        this.pageNum = pageNum
        this.load()
      },
      load () {
        fetch("http://localhost:9091/book/page?pageSize=" + this.pageSize + "&pageNum=" + this.pageNum + "&bookName=" + this.bookName).then(res => res.json()).then(res => {
          console.log(res.total)
          console.log(res)
          console.log("hello")
          this.tableData = res.data
          this.total = res.total
        })
      }
    }
  }
</script>