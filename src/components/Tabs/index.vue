<template>
  <el-tabs type="border-card" class="tab-wrap">
    <el-tab-pane label="普通加密">
      <encrypt-panel />
    </el-tab-pane>
    <el-tab-pane label="普通加签">
      <signature-panel />
    </el-tab-pane>
    <el-tab-pane label="指数/模数加密">
      <pem-panel />
    </el-tab-pane>
    <el-tab-pane label="降级加密">
      <security-panel />
    </el-tab-pane>
  </el-tabs>
</template>

<script setup>
import EncryptPanel from './EncryptPanel.vue'
import SignaturePanel from './SignaturePanel.vue'
import PemPanel from './PemPanel.vue'
import SecurityPanel from './SecurityPanel.vue'

</script>

<style scoped>

</style>
