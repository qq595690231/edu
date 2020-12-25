<template>
  <div class="role-list">
    <el-card class="box-card">
      <div slot="header" class="clearfix">
        <el-form ref="form" :model="form">
          <el-form-item label="角色名称">
            <el-input v-model="form.name"></el-input>
          </el-form-item>
          <el-form-item>
            <el-button
              type="primary"
              @click="onSubmit"
              v-loading="isLoading"
            >查询</el-button>
            <el-button @click="onReset">重置</el-button>
          </el-form-item>
        </el-form>
      </div>
      <el-button>添加角色</el-button>
      <el-table
        :data="roles"
        style="width: 100%"
        v-loading="isLoading"
      >
        <el-table-column
          prop="id"
          label="编号"
        />
        <el-table-column
          prop="name"
          label="角色名称"
        />
        <el-table-column
          prop="description"
          label="描述"
        />
        <el-table-column
          prop="createdTime"
          label="添加时间"
        />
        <el-table-column
          label="操作"
          align="center"
          width="150px"
        >
          <template slot-scope="scope">
            <div>
              <el-button
                type="text"
              >分配菜单</el-button>
              <el-button
                type="text"
              >分配资源</el-button>
            </div>
            <div>
              <el-button
                type="text"
                @click="handleEdit(scope.row)"
              >编辑</el-button>
              <el-button
                type="text"
                @click="handleDelete(scope.row)"
              >删除</el-button>
            </div>
          </template>
        </el-table-column>
      </el-table>
    </el-card>
  </div>
</template>

<script>
// 引入请求方法
import { getRoles, deleteRole } from '@/services/role'

export default {
  name: 'RoleList',
  data () {
    return {
      form: {
        name: ''
      },
      isLoading: false,
      roles: []
    }
  },
  created () {
    this.loadRoles()
  },
  methods: {
    onReset () {

    },
    onSubmit () {

    },
    handleEdit (role) {

    },
    // 删除角色
    handleDelete (role) {
      this.$confirm(`确认删除角色：${role.name}？`, '删除提示')
        .then(async () => {
          await deleteRole(role.id)
          this.$message.success('删除成功')
          this.loadRoles()
        })
        .catch(err => {
          if (err && err.response) {
            this.$message.error('删除失败，请重试')
          } else {
            this.$message.info('取消删除')
          }
        })
    },
    // 请求角色列表数据
    async loadRoles () {
      this.isLoading = true
      const { data } = await getRoles(this.form)
      this.roles = data.data.records
      this.isLoading = false
    }
  }
}
</script>

<style lang="scss" scoped></style>
