<template>
  <panel v-bind="post" v-on="action" />
</template>
<script setup>
import Panel from '../Panel.vue'
import { reactive, defineProps, computed } from 'vue'
import { JSEncrypt } from 'jsencrypt'
import { publickey, privateKey } from '../../constants'

const state = reactive({ 
  encrypt: '',  // 待加密数据
  encryptRes: '',  // 加密结果
  decrypt: '',  // 待解密数据
  decryptRes: ''  // 解密结果
})

// 传递子组件prop
const post = computed(()=>({
  title: '使用 jsencrypt.js 插件',
  encrypt: state.encrypt,
  encryptRes: state.encryptRes,
  decrypt: state.decrypt,
  decryptRes: state.decryptRes,
}))

// 加密
const onEncrypt = () => {
  let msg = state.encrypt
  const jsencrypt = new JSEncrypt()
  jsencrypt.setPublicKey(publickey)
  state.encryptRes = jsencrypt.encrypt(msg)
}

// 解密
const onDecrypt = () => {
  let msg = state.decrypt
  let decrypt = new JSEncrypt()
  decrypt.setPrivateKey(privateKey)
  var decryptMsg = decrypt.decrypt(msg)
  state.decryptRes = decryptMsg
}

// 监听子组件事件
const action = {
  'update-encrypt': (value) => state.encrypt = value,
  'click-encrypt': onEncrypt,
  'update-decrypt': (value) => state.decrypt = value,
  'click-decrypt': onDecrypt,
}

</script>
