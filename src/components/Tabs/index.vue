<template>
  <el-tabs type="border-card" class="tab-wrap">
    <el-tab-pane label="普通加密/解密">
      <encrypt-panel />
    </el-tab-pane>
    <el-tab-pane label="使用加签">
      <encrypt-panel />
    </el-tab-pane>
    <el-tab-pane label="指数模数加密">
      <encrypt-panel />
    </el-tab-pane>
  </el-tabs>
</template>

<script setup>
import EncryptPanel from './EncryptPanel.vue'

</script>

<style scoped>

</style>
