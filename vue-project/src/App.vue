<script>
  export default {
    data() {
      return{
        output : null,
        prev : null,
        cur : null,
        operator : null,
      };
    },
    methods: {
      operation(e){
        const number = e.currentTarget.value;
        if (['+', '-', '*', '/', '='].includes(number)) {
          //사칙 연산 기호면 연산 로직 구현
          this.output = null;
          this.operator = number;
          this.prev = Number(this.cur);
          this.cur = null;
          return;
        }

        //사용자가 입력한 숫자(실제로는 문자열임)저장
        this.cur = this.cur === null ? number:(this.cur+=number);

        //입력한 값이 출력칸(output) 안에 표시되도록 output 데이터에 저장
        this.output = this.cur;
      },
    },
  }
</script>

<template>
  <div class="calculator">
      <form name="forms">
        <!-- v-model 디렉티브를 사용해 output 데이터를 양방향으로 바인딩 -->
        <input v-model="output" type="text" name="output" readonly />
        <input type="button" class="clear" value="C" @click="operation"/>
        <input type="button" class="operator" value="/" @click="operation"/>
        <input type="button" value="1" @click="operation"/>
        <input type="button" value="2" @click="operation"/>
        <input type="button" value="3" @click="operation"/>
        <input type="button" class="operator" value="*" @click="operation"/>
        <input type="button" value="4" @click="operation"/>
        <input type="button" value="5" @click="operation"/>
        <input type="button" value="6" @click="operation"/>
        <input type="button" class="operator" value="+" @click="operation"/>
        <input type="button" value="7" @click="operation"/>
        <input type="button" value="8" @click="operation"/>
        <input type="button" value="9" @click="operation"/>
        <input type="button" class="operator" value="-" @click="operation"/>
        <input type="button" class="dot" value="." @click="operation"/>
        <input type="button" value="0" @click="operation"/>
        <input type="button" class="operator result" value="=" @click="operation"/>
      </form>
    </div>
</template>

<style>
@import './assets/style.css';
</style>
