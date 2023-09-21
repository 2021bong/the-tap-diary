<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'DateModal',
  emits: ['show-modal'],
  props: {
    lan: Boolean
  },
  setup(_, { emit }) {
    const clickHideModalBtn = () => {
      emit('show-modal');
    };

    return { clickHideModalBtn };
  },
});
</script>

<template>
  <div class="background">
    <div class="date-modal">
      <h4 class="title">월별로 보기</h4>
      <div class="month-box"></div>
      <button class="close-btn" @click="clickHideModalBtn">
        <span
          class="pi pi-times icon"
          style="font-size: 1.2rem; color: #000"
        ></span>
      </button>    </div>
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
.date-modal {
  position: absolute;
  top: 20%;
  left: calc(50% - 200px);
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 400px;
  height: 500px;
  padding: 40px 20px;
  background-color: #fdfdfd;
  border-radius: 20px;
  box-shadow: 1px 7px 14px 3px rgba(0, 0, 0, 0.25);
  box-sizing: border-box;

  .title {
    font-size: 18px;
    margin-bottom: 30px;
  }

  .month-box{
    width: 100%;
    height: 70%;
    margin-bottom: 30px;
    border: 1px solid red;
  }
  .close-btn {
    position: absolute;
    left: calc(50% - 20px);
    bottom: 30px;
    margin: 10px;
    background-color: #fff;
    transition: 0.2s;

    &:hover {
      padding: 10px;
      transform: translateY(10px) translateX(-5px);
      background-color: #eee;
    }
  }
}
</style>
