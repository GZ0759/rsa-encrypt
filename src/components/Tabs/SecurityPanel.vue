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

const onMounted = () => {
  console.log('Component is mounted!')
}

import('../../utils/security.js')

// 传递子组件prop
const post = computed(()=>({
  title: '使用 security.js 在全局进行绑定',
  encryptText: '加密',
  encrypt: state.encrypt,
  encryptRes: state.encryptRes,
  decryptText: '解密',
  decrypt: state.decrypt,
  decryptRes: state.decryptRes,
}))

// 加密
const onEncrypt = () => {
  let msg = state.encrypt
  let exponent = '9E80B2BD4C1C3610F04B809EA52CD4E92FC54A3D64DD64DA824195B8A0D726A87318A180C20CB56613B92A1488D1DA59B8CAEF64BDE1A958EBF8E8EF94181B5D'
  let modulus = '0x10001'
  let key = new window.RSAUtils.getKeyPair(exponent, "", modulus)
  let apwd = window.RSAUtils.encryptedString(key, msg);
  state.encryptRes = apwd
}

// 解密
const onDecrypt = () => {
  let msg = state.decrypt
  let key = privateKey
  let apwd = window.RSAUtils.decryptedString(key, msg);
  state.decryptRes = apwd
}

// 监听子组件事件
const action = {
  'update-encrypt': (value) => state.encrypt = value,
  'click-encrypt': onEncrypt,
  'update-decrypt': (value) => state.decrypt = value,
  'click-decrypt': onDecrypt,
}

</script>
