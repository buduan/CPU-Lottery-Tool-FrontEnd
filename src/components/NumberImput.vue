<script setup>
defineEmits(['enlarge-text'])
</script>

<template>
  <div>
    <div class="">
        <input class="w-80 p-8 h-20 text-3xl my-2 montserrat font-bold text-neutral-900 rounded-xl border-2 empty:border-slate-400  focus:border-gray-900" v-model="inputValue" type="text" placeholder="输入抽奖码^_^" />
        <button class="transition ease-in-out size-20 p-6 text-3xl ml-4 montserrat font-medium text-slate-50 bg-red-500 rounded-xl hover:bg-red-950" @click="clearInput"> C </button>   
    </div>

    <div class="grid grid-cols-5 gap-4 my-8">
      <button 
      class="transition ease-in-out text-2xl size-20 p-12 montserrat font-medium bg-slate-200 rounded-xl hover:bg-slate-900 hover:text-slate-50 hover:text-3xl"
      v-for="num in 9" :key="num" @click="addNumber(num)">
        {{ num }}
      </button>
      <button 
      class="transition ease-in-out p-12 size-20 text-2xl montserrat font-medium bg-slate-200 rounded-xl hover:bg-slate-900 hover:text-slate-50 hover:text-3xl"
      key="0" @click="addNumber(0)">
        0
      </button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      inputValue: '',
    };
  },
  methods: {
    addNumber(num) {
        this.inputValue += num;
        if (this.inputValue.length >= 8) {
            console.log("Student id number is",this.inputValue);
            this.$emit('showModel', this.inputValue);
            this.inputValue = "";
        }
    },
    clearInput() {
        this.inputValue = "";
    },
    inputStatus() {
        console.log(this.inputValue)
    }
  },
};
</script>

<style scoped>

button {
  padding: 5px 10px;
}
</style>