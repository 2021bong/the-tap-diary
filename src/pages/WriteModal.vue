<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({});
</script>

<template>
  <div class="background">
    <div class="write-modal">
      <h4 class="title">작성하기</h4>
    </div>
  </div>
</template>

<style lang="scss" scoped>
.background {
  position: absolute;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  background-color: rgba(0, 0, 0, 0.1);
}
.write-modal {
  position: absolute;
  top: 25%;
  left: calc(50% - 200px);
  display: flex;
  justify-content: center;
  width: 400px;
  height: 300px;
  padding: 20px;
  background-color: #fdfdfd;
  border-radius: 20px;
  box-shadow: 1px 7px 14px 3px rgba(0, 0, 0, 0.25);

  .title {
    font-size: 18px;
  }
}
</style>
