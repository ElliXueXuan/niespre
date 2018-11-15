<template>
<div class="menu-wrap" :style="{minHeight:minHeight+'px'}">
  <el-row :style="{minHeight:minHeight+'px'}">
    <el-col :span="4" style="" class="my-list">
      <el-menu style="" router :default-active="defaultActive" @select="handleSelect">
        <el-submenu index="1">
          <template slot="title">
            <span class="my-left-border"></span>设置训练数据
          </template>
          <el-menu-item index="/result/train">训练集</el-menu-item>
          <el-menu-item index="/result/validate">验证集</el-menu-item>
          <el-menu-item index="/result/new">新进化合物</el-menu-item>
        </el-submenu>
        <el-menu-item index="/forecast"><span class="my-left-border"></span>化学品毒性预测</el-menu-item>
      </el-menu>
    </el-col>
    <el-col :span="20" :style="{minHeight:minHeight+'px'}" class="overFlow">
      <router-view></router-view>
    </el-col>
  </el-row>
</div>
</template>

<script>
export default {
  data() {
    return {
      defaultActive: '',
      selectIndex: '',
      minHeight: 0
    }
  },
  created() {
    this.defaultActive = this.$route.fullPath;
    this.selectIndex = this.defaultActive;
  },
  mounted() {
    this.minHeight = document.documentElement.clientHeight - 72 - 90 - 50; // 72:fotter高度；50 header高度 ；50 menu的margin
    let that = this;
    window.onresize = function() {
      that.minHeight = document.documentElement.clientHeight - 72 - 90 - 50;
    }
  },
  methods: {
    handleSelect(index, indexPath) {
      this.selectIndex = index;
    }
  }

}
</script>

<style>
/* background-color: rgba(228, 228, 228, 1); */

.menu-wrap {
  margin: 50px 50px 0;
  background-color: #fff;
}

.menu-wrap .el-row {
  /*min-height: 530px;*/
}

.menu-wrap .overFlow {
  overflow-y: auto;
  overflow-x: hidden;
}

.menu-wrap .el-menu-item {
  padding-left: 80px;
}

.menu-wrap .el-menu-item.is-active {
  color: #fff;
  background-color: #409eff;
}
</style>
