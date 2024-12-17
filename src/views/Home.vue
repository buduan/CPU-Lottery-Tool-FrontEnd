<template>
  <div id="app">
    <div>
      <div class="my-8 ">
        <h1 class="text-4xl my-2 font-bold text-slate-900">
        填写申请表单后，<br>即可在此参与抽奖！
        </h1>
        <span class="text-gray-600 my-2">请在屏幕上输入抽奖码参与抽奖</span>
      </div>
      <NumberInput @showModel="drewGift"/>
    </div>
    
    <div class="absolute left-0 top-0 w-screen h-screen bg-slate-500/20 backdrop-blur-md content-center" v-show="popup">
      <div class="max-w-[48rem] max-h-96 bg-white rounded-3xl p-16 px-auto text-center mx-auto">
        <h1 class="text-4xl font-bold noto-sans-sc text-red-500 ">{{drewTitle}}</h1>
        <h2 class="text-2xl font-medium noto-sans-sc my-4">{{drewName}}</h2>
        <hr class="my-8">
        <span class="my-4"> 
          请及时联系摊位工作人员领奖，<span class="underline decoration-red-500">请勿重复领奖</span>，感谢您的合作。 <br>
          抽奖结果即时有效，无特殊情况<span class="underline decoration-red-500">请立刻兑奖</span>，离开摊位后<span class="underline decoration-red-500">立即失效</span>！
         </span>
         <button @click="popup = !popup" class="block w-10 p-2 bg-red-100 rounded-lg my-4 mx-auto text-red-500"> ✕ </button>
      </div>
    </div>
  </div>
</template>

<script>
import { popScopeId, watch } from 'vue';
import NumberInput from '../components/NumberImput.vue';


export default {
  name: 'App',
  components: {
    NumberInput,
  },
  watch: {

  },
  data (){
    return{
      popup: false, //true, 自动弹出抽奖框
      drewTitle: '请等待开奖...',
      drewName: '开奖中'
    }
  },
  created() {

  },
  methods: {
    async handleShowModel(inputValue) {
      this.popup = true; // 设定 popup 状态
      await this.drewGift(inputValue); // 调用 drewGift 方法，并传递 inputValue
    },
    async drewGift(value) {
      try {
        const response = await fetch(`http://cpu.gift.ibuduan.com/gift/drew/${value}`);
        if (!response.ok) {
          throw new Error('Network response was not ok');
        }
        const data = await response.json();
        this.handleApiResponse(data); // 处理返回的数据
      } catch (error) {
        console.error('There has been a problem with your fetch operation:', error);
      }
    },
    handleApiResponse(data) {
      if (data.message === '抽奖成功') {
        this.popup = true;
        console.log('抽奖成功！');
        console.log('申请者姓名:', data.applicant);
        console.log('学号:', data.studentId);
        console.log('抽中的礼品标题:', data.gift);
        this.drewTitle = "恭喜你，" + data.applicant + "! 获得：" + data.gift
        console.log('礼品名称:', data.name);
        this.drewName = data.name
        // 可以在这里进行其他处理，例如显示抽奖结果
      } else {
        console.error('抽奖失败:', data.message);
        // 可以在这里处理错误信息，例如显示失败消息
      }
    }
  }
  
  
};
</script>

<style>

#app {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}
</style>