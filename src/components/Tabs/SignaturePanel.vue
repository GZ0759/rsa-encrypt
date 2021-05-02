<template>
  <panel v-bind="post" v-on="action" />
</template>
<script setup>
import Panel from '../Panel.vue'
import { reactive, defineProps, computed } from 'vue'
import Jsrsasign from 'jsrsasign'
import { publickey, privateKey } from '../../constants'

const state = reactive({ 
  encrypt: '',  // 待加密数据
  encryptRes: '',  // 加密结果
  decrypt: '',  // 待解密数据
  decryptRes: ''  // 解密结果
})

// 传递子组件prop
const post = computed(()=>({
  title: '使用 jsrsasign.js 插件进行加签',
  encryptText: '加签',
  encrypt: state.encrypt,
  encryptRes: state.encryptRes,
  decryptText: '解签',
  decrypt: state.decrypt,
  decryptRes: state.decryptRes,
}))

// 私钥加签
const onEncrypt = () => {
  let msg = state.encrypt
  let { KJUR, hex2b64, KEYUTIL } = Jsrsasign
  let sig = new KJUR.crypto.Signature({"alg": "SHA1withRSA"})
  sig.init(privateKey)
  sig.updateString('aaa')
  state.encryptRes = hex2b64(sig.sign())
  // 普通RSA加密
  // let res = KJUR.crypto.Cipher.encrypt(msg, KEYUTIL.getKey(publickey))
  // state.encryptRes = hex2b64(res)
}

// 公钥解签
const onDecrypt = () => {
  let msg = state.decrypt
  let { KJUR, b64tohex, KEYUTIL } = Jsrsasign
  let sig = new KJUR.crypto.Signature({"alg": "SHA1withRSA"})
  sig.init(publickey)
  sig.updateString('aaa')
  state.decryptRes = sig.verify(b64tohex(msg))
  // 普通RSA解密
  // let res = KJUR.crypto.Cipher.decrypt(b64tohex(msg), KEYUTIL.getKey(privateKey))
  // state.decryptRes = res
}

// 监听子组件事件
const action = {
  'update-encrypt': (value) => state.encrypt = value,
  'click-encrypt': onEncrypt,
  'update-decrypt': (value) => state.decrypt = value,
  'click-decrypt': onDecrypt,
}

</script>
