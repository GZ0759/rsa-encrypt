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
  let exponent = '00b812820160ab71866d71f026b363c1c9a61f1e84e0134e143790db8aa37057d0b3fc95780e8a048ca187605312a8a62ee52c18bb846c4e6b4768a096d4145903f2ba1632f6adae25961167d67ac773993e59ef3437392be1da00bcf2da9b2d63bc4f8993fb61cbbd06a70d95ea99fd4749c92f4933807863890103649918b527'
  let modulus = '010001'
  let key = new RSAUtils.getKeyPair(exponent, "", modulus)
  console.log('key', key);
  let apwd = RSAUtils.encryptedString(key, msg);
  state.encryptRes = apwd

  // let msg = state.encrypt
  // const jsencrypt = new JSEncrypt()
  // jsencrypt.setPublicKey(publickey)
  // state.encryptRes = jsencrypt.encrypt(msg)
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
