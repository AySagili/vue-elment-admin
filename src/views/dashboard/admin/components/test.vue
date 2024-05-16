<template>
  <el-row :gutter="20">
    <el-col :span="12">
      <div class="grid-content">你好</div>
    </el-col>
    <el-col :span="12">
      <div class="grid-content">你好</div>
    </el-col>
    <el-row>
        
    </el-row>
  </el-row>
</template>
 
<style scoped>
.el-row {
  margin-bottom: 20px;
  background-color: red;
  border-radius: 4px;
  min-height: 36px;
  line-height: 36px;
}
.el-col {
  border-radius: 4px;
}
.grid-content {
  border-radius: 4px;
  min-height: 36px;
  line-height: 36px;
  text-align: center;
}
</style>