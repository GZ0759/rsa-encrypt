<template>
  <el-card class="box-card">
    <template #header>
      <div class="card-header">
        <span>{{ title }}</span>
      </div>
    </template>
    <el-row :gutter="20">
      <el-col :span="22">
        <div class="box">
          <el-input :modelValue="encrypt" @input="$emit('update-encrypt', $event)" :placeholder="'请输入'+encryptText+'内容'" ></el-input>
        </div>
      </el-col>
      <el-col :span="2">
        <el-button type="primary" @click="$emit('click-encrypt')" >{{ encryptText }}</el-button >
      </el-col>
    </el-row>
    <el-row :gutter="20">
      <el-col :span="24">
        <div class="res">{{ encryptRes || '结果' }}</div>
      </el-col>
    </el-row>
    <el-row :gutter="20">
      <el-col :span="22">
        <div class="box">
          <el-input :modelValue="decrypt" @input="$emit('update-decrypt', $event)" :placeholder="'请输入'+decryptText+'内容'" ></el-input>
        </div>
      </el-col>
      <el-col :span="2">
        <el-button type="danger" @click="$emit('click-decrypt')" >{{ decryptText }}</el-button >
      </el-col>
    </el-row>
    <el-row :gutter="20">
      <el-col :span="24">
        <div class="res">{{ decryptRes || '结果' }}</div>
      </el-col>
    </el-row>
  </el-card>
</template>

<script setup>
import { reactive, defineProps } from 'vue'

const prop = defineProps({
  title: String,
  encryptText: String,
  encrypt: String,
  encryptRes: String,
  decryptText: String,
  decrypt: String,
  decryptRes: [String, Boolean],
})

</script>

<style scoped>
.box-card {
  min-height: 40vh;
  padding: .4rem .6rem;
}
.res {
  height: 2.2rem;
  text-align: left;
  margin: 1rem 0 2rem;
  padding: 0 .8rem;
  word-break: break-all;
}
</style>
