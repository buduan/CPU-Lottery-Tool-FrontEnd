<script setup>
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
  <div class="w-1/3 mr-12">
    <h1 class="my-8 text-4xl font-black text-slate-900 nomo-sans-sc text-center"> 扫描二维码<br>加入我们</h1>
    <img src="/src/assets/qrcode.png" class="my-8 mx-auto w-64 h-64 p-4 rounded-3xl border-4 border-yellow-400">
    <p class="w-96 mx-auto text-sm">
      *填写表单即代表您同意我们根据《Microsoft 隐私声明》《UNNC Privacy Policy》《不断同学创意网络科技工作室隐私数据处理协议》对您所输入的数据进行处理。 <br>
      **我们可能会根据后续需要公开、分享您的部分数据以做学习评估使用，感谢您的理解。
    </p>
  </div>
  <RouterView />
</template>

<style>
h1,h2,h3,h4,h5,h6,p,span{
  @apply leading-normal !important;

}

</style>
