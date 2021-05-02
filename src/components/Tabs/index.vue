<template>
  <el-tabs type="border-card" class="tab-wrap">
    <el-tab-pane label="普通加密">
      <encrypt-panel />
    </el-tab-pane>
    <el-tab-pane label="普通加签">
      <encrypt-sign-panel />
    </el-tab-pane>
    <el-tab-pane label="指数/模数加密">
      <encrypt-panel />
    </el-tab-pane>
    <el-tab-pane label="降级加密">
      <encrypt-panel />
    </el-tab-pane>
  </el-tabs>
</template>

<script setup>
import EncryptPanel from './EncryptPanel.vue'
import EncryptSignPanel from './SignaturePanel.vue'

</script>

<style scoped>

</style>
