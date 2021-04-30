<template>
  <h1>{{ msg }}</h1>
  <div class="rsa-wrap">
    <div class="box">
      <el-input v-model="state.encrypt" placeholder="请输入加密内容"></el-input>
      <el-button type="primary" @click="onEncrypt(state.encrypt)">加密</el-button>
    </div>
    <div class="res">{{ state.encryptRes || '---' }}</div>
    <div class="box">
      <el-input v-model="state.decrypt" placeholder="请输入解密内容"></el-input>
      <el-button type="danger" @click="onDecrypt(state.decrypt)">解密</el-button>
    </div>
    <div class="res">结果：{{ state.decryptRes }}</div>
  </div>
</template>

<script setup>
import { defineProps, reactive } from 'vue'
import { JSEncrypt } from 'jsencrypt'
import { publickey, privateKey } from '../constants'
 
defineProps({
  msg: String
})
  
const state = reactive({ 
  encrypt: '',
  encryptRes: '',
  decrypt: '',
  decryptRes: ''
})

// 加密
const onEncrypt = (msg) => {
  const jsencrypt = new JSEncrypt()
  jsencrypt.setPublicKey(publickey)
  state.encryptRes = jsencrypt.encrypt(msg)
}
 
// 解密
const onDecrypt = (msg) => {
  let decrypt = new JSEncrypt()
  decrypt.setPrivateKey(privateKey)
  var decryptMsg = decrypt.decrypt(msg)
  state.decryptRes = decryptMsg
}

</script>

<style scoped>
.rsa-wrap {
  width: 60vw;
  margin: 0 auto;
}
.box {
  display: flex;
  margin: .8rem 0;
}
.res {
  height: 2.2rem;
  text-align: left;
  margin: 1rem 0 2rem;
  padding: 0 .8rem;
  word-break: break-all;
}
</style>
