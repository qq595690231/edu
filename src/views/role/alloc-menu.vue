<template>
  <div class="alloc-menu">
    <el-card>
      <el-tree
        :data="menus"
        :props="defaultProps"
        show-checkbox
        default-expand-all
      ></el-tree>
    </el-card>
  </div>
</template>

<script>
import { getMenuNodeList } from '@/services/menu'
export default {
  name: 'AllocMenu',
  props: {
    roleId: {
      type: [Number, String],
      required: true
    }
  },
  created () {
    this.loadMenus()
  },
  data () {
    return {
      menus: [],
      defaultProps: {
        children: 'subMenuList',
        label: 'name'
      }
    }
  },
  methods: {
    async loadMenus () {
      const { data } = await getMenuNodeList()
      if (data.code === '000000') {
        this.menus = data.data
      }
    }
  }
}
</script>

<style lang="scss" scoped></style>
