<template>
  <div>
    <el-breadcrumb separator-class="el-icon-arrow-right">
      <el-breadcrumb-item :to="{ path: '/' }">首页</el-breadcrumb-item>
      <el-breadcrumb-item>用户管理</el-breadcrumb-item>
      <el-breadcrumb-item>用户列表</el-breadcrumb-item>
    </el-breadcrumb>
    <el-card class="box-card">
      <el-row :gutter="20">
        <el-col :span="8">
          <div class="grid-content bg-purple">
            <el-input placeholder="请输入内容" v-model="userlist.query" class="input-with-select">
              <el-button slot="append" icon="el-icon-search"></el-button>
            </el-input>
          </div>
        </el-col>
        <el-col :span="8">
          <div class="grid-content bg-purple-light">
            <el-button type="primary">主要按钮</el-button>
          </div>
        </el-col>
      </el-row>

      <el-table stripe border :data="userlist" style="width: 100%">
        <el-table-column prop="username" label="用户名" width="180"></el-table-column>
        <el-table-column prop="email" label="邮箱" width="180"></el-table-column>
        <el-table-column prop="mobile" label="手机号" width="180"></el-table-column>
        <el-table-column prop="create_time" label="用户注册时间" width="180">
            <!-- <template slot-scope="user">
               {{user.row.create_time | fmt('YYYY-MM-DD HH:mm:ss') }}
            </template> -->
        </el-table-column>
        <el-table-column prop="mg_state" label="状态" width="180"></el-table-column>
        <el-table-column prop="mg_state" label="操作"></el-table-column>
      </el-table>
    </el-card>
  </div>
</template>

<script>
export default {
     filters:{
        shiJi:function(v,fromsj){
            return moment(v).format(fromsj)
        }
  },
  created() {
    this.getList()
  },
 
  methods: {
    async getList() {
      const {
        data: {
          data,
          meta: { msg, status }
        }
      } = await this.$http.get('/users', { params: this.togo })
      console.log(data, msg, status)
      if (status === 200) {
        this.userlist = data.users
      }
    }
  },
  data() {
    return {
      userlist: [],

      togo: {
        query: '',
        pagenum: 1,
        pagesize: 3
      }
    }
  }
}
</script>

<style lang="less">
.el-main {
  div {
    .el-card {
      margin-top: 20px;
    }
  }
}
</style>
