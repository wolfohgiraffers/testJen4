<template>
  <div class="plus">
    <h1>덧셈 기능 만들기</h1>
    <label>num1: </label><input type="text" v-model="num1">&nbsp;
    <label>num2: </label><input type="text" v-model="num2">&nbsp;
    <button @click="sendPlus">더하기</button><br>
    <hr>
    <p>`{{ num1 }} + {{ num2 }} = {{ result }}`</p>
    <pre>{{ tt }}</pre>
  </div>
</template>

<script setup>
  import {ref} from 'vue';

  const num1 = ref(0);
  const num2 = ref(0);
  const result = ref(0);
  const tt = ref('');

  const sendPlus = async() => {

    // 다른 컨테이너의 외부 접속 포트로 접근한다.
    // const response = await fetch(`http://localhost:5173/api/plus?num1=${num1.value}&num2=${num2.value}`);
    const response = await fetch(`http://localhost:30001/plus?num1=${num1.value}&num2=${num2.value}`);
    // const response = await fetch(`http://localhost:8055/plus?num1=${num1.value}&num2=${num2.value}`);
    // const response = await fetch(`http://localhost:8011/api/plus?num1=${num1.value}&num2=${num2.value}`);
    const data = await response.json();
    result.value = data.sum;
  }
</script>

<style scoped>
  .plus {
    text-align: center;
  }
</style>