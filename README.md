# RSA 加密与解密

## 加密与加签

### 加密：数据传输的安全性

RSA 加密解密主要应用于数据传输的安全性上。通过公钥加密、私钥解密的方式，可以达到公钥持有者能够加密数据，但只有私钥持有者才能够解密数据。通过加密传输数据能够避免被第三方截取者轻易的拦截数据，而通过 RSA 非对称加密的特性也能够较好的保证第三方截取者在没有私钥的情况下读取数据内容。

### 加签：数据的防篡改、防否认机制

数据的的防否认机制是指数据的接收者可以明确的知道数据的发送人。RSA 的数字签名技术是将摘要信息用发送者的私钥（有且只有一人持有）加密，与原文一起传送给接收者。接收者只有用发送者的公钥才能解密被加密的摘要信息，然后用 HASH 函数对收到的原文产生一个摘要信息，与解密的摘要信息对比。如果相同，则说明数据是有持有私钥的发送者发出的（其他人没有私钥，无法生成一致的摘要信息）。因此在此基础上可以认为有且只有一个私钥的持有者才可以加签，达到数据的防止篡改防否认机制。

## 辅助工具

- [Vue 3](https://v3.cn.vuejs.org/)
- [Vite](https://cn.vitejs.dev/)
- [element-plus](https://element-plus.gitee.io/#/zh-CN)
- [生成 RSA 密钥对](http://web.chacuo.net/netrsakeypair)
