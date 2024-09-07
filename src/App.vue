<!-- js -->
<script setup>
import { ref } from 'vue';

/**
 * todo item
 * key: text, done
 * item.text or item['text']
 * 
 * {
 *   text: string,
 *   done: boolean(true/false)
 * }
**/

// 반응형 데이터
const inputValue = ref('');
const todoList = ref([
  { text: 'vue', done: false },
  { text: 'react', done: false },
  { text: 'vercel', done: false }
]);

console.log(todoList.value);

// 새로운 할 일 추가 함수
const handleClickButton = () => {
  if (inputValue.value.trim() !== '') {
    todoList.value.push({ text: inputValue.value, done: false });
    inputValue.value = '';  // 입력 필드 초기화
  }
};

// 삭제 버튼 클릭 시 실행되는 함수
const handleClickDeleteButton = (index) => {
  todoList.value.splice(index, 1);  // 해당 항목 삭제
};
</script>

<!-- html -->
<template>
  <h4>TODO LIST</h4>

  <!-- 입력 필드 -->
  <input v-model="inputValue" placeholder="할 일을 입력하세요" />
  <p>{{ inputValue }}</p>

  <!-- 확인 버튼 -->
  <button @click="handleClickButton">확인</button>

  <!-- TODO 항목 목록 -->
  <div class="todo-item" v-for="(item, index) in todoList" :key="index">
    <input type="checkbox" v-model="item.done" />
    <span :class="{'done-item': item.done}">{{ item.text }}</span>
    <button>수정</button>
    <button @click="handleClickDeleteButton(index)">삭제</button>
  </div>
</template>

<!-- css -->
<style scoped>
.todo-item {
  width: 100%;
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
  border: 1px solid gray;
  padding: 5px;
  margin-bottom: 5px;
}

.done-item {
  text-decoration: line-through; /* 완료된 항목은 줄을 긋습니다 */
  color: gray;
}
</style>
