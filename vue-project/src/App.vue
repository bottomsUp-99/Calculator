<script>
  export default {  // Vue 컴포넌트를 정의하는 부분
    data() {  // 컴포넌트에서 사용하는 데이터 반환
      return {
        output: null,  // 현재 출력될 값을 저장
        prev: null,  // 이전에 입력한 숫자 또는 계산 결과를 저장
        cur: null,  // 현재 입력 중인 숫자를 저장
        operator: null,  // 선택된 연산자를 저장 (+, -, *, / 등)
      }  
    },
    methods: {
      operation(e) {  // 버튼 클릭 시 호출되는 메서드 (계산 처리)
        const number = e.currentTarget.value;  // 클릭된 버튼의 value 값을 가져옴 (숫자 또는 연산자)

        if (number === 'C') {  // 'C' 버튼이 눌리면 모든 값을 초기화 (clear)
          this.output = null;
          this.prev = null;
          this.cur = null;
          this.operator = null;
          return;  // 초기화 후 메서드를 종료
        }

        if (['+', '-', '*', '/', '='].includes(number)) {  // 입력된 값이 연산자나 '='인 경우
          if (!this.cur && !this.prev) {  // 현재 값과 이전 값 모두 없을 때 연산자가 눌리면 경고 표시
            alert('숫자를 먼저 입력하세요.');
            return;
          }

          if (this.operator !== '' && !this.cur) {  // 연산자가 연속으로 눌릴 경우 경고 표시
            alert('사칙연산 기호를 연달아 누를 수 없습니다.');
            return;
          }
           
          if (number === '=' && this.prev === this.cur) {  // '='가 눌렸지만 현재 값과 이전 값이 같은 경우는 계산하지 않음
            return;
          }
          
          this.cur = Number(this.cur);  // 현재 입력된 값을 숫자로 변환 (문자열을 숫자로)

          if (this.operator != null) {  // 연산자가 선택된 상태라면 (계산을 진행)
            switch (this.operator) {  // 연산자에 따라 계산 수행
              case '+':
                this.prev = this.prev + this.cur;  // 덧셈 연산
                break;
              case '-':
                this.prev = this.prev - this.cur;  // 뺄셈 연산
                break;
              case '*':
                this.prev = this.prev * this.cur;  // 곱셈 연산
                break;
              case '/':
                this.prev = this.prev / this.cur;  // 나눗셈 연산
                break;
            }

            if (number === '=') {  // '='가 눌린 경우
              this.output = this.prev;  // 계산 결과를 출력으로 설정
              this.operator = null;  // 연산자를 초기화
              this.cur = this.prev;  // 현재 값을 계산 결과로 설정
            } else {  // '='가 아닌 경우 (다음 연산 준비)
              this.output = null;  // 출력 값을 초기화
              this.operator = number;  // 새로운 연산자를 설정
              this.cur = null;  // 현재 값을 초기화
            }

          } else {  // 처음 연산자가 선택된 경우
            this.output = null;  // 출력 값을 초기화
            this.operator = number;  // 연산자를 설정
            this.prev = this.cur;  // 현재 값을 이전 값으로 설정
            this.cur = null;  // 현재 값을 초기화
          }
          return;  // 메서드 종료
        }
                 
        // 사용자가 입력한 숫자(실제로는 문자열)를 저장
        this.cur = this.cur === null ? number : (this.cur += number);
                 
        // 입력한 값이 출력창에 표시되도록 output 데이터에 저장
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
