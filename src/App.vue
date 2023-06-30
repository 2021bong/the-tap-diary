<script setup lang="ts">
import Month from './components/Month.vue';
</script>

<template>
  <div>
    <button class="korean_lan btn">한국어</button>
    <button class="english_lan btn">English</button>
    <h1 class="title">맨날 우는 사람이 우는 이유</h1>
    <p class="desc">오늘은 또 무슨 이유로 울었을까요? 🥲</p>
  </div>
  <Month />
</template>

<style scoped lang="scss">
.btn {
  width: 100px;

  &:first-of-type {
    margin-right: 10px;
  }
}
.title {
  margin: 10px 0;
  font-weight: 800;
}

.desc {
  display: inline-block;
  margin-bottom: 10px;
  padding: 5px 20px;
  background-color: #dfe9f5;
  border-radius: 16px;
}
</style>
