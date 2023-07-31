<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'WriteModal',
  emits: ['show-modal'],
  setup(_, { emit }) {
    const tearLevel = [
      { level: '울컥', class: 'level1', select: true },
      { level: '글썽', class: 'level2', select: true },
      { level: '또르륵', class: 'level3', select: true },
      { level: '주륵주륵', class: 'level4', select: true },
      { level: '꺼이꺼이', class: 'level5', select: true },
    ];
    const clickHideModalBtn = () => {
      emit('show-modal');
    };

    return { tearLevel, clickHideModalBtn };
  },
});
</script>

<template>
  <div class="background">
    <div class="write-modal">
      <h4 class="title">작성하기</h4>
      <ul class="level-box">
        <li
          v-for="levelData in tearLevel"
          class="level"
          :class="
            levelData.select ? levelData.class + ' select' : levelData.class
          "
          :id="levelData.class"
        >
          {{ levelData.level }}
        </li>
      </ul>
      <button class="close-btn" @click="clickHideModalBtn">
        <span
          class="pi pi-times icon"
          style="font-size: 1.2rem; color: #000"
        ></span>
      </button>
      <div class="text-area">
        <textarea
          name="reason"
          id="reason"
          placeholder="오늘 또 운 이유는 ?"
        ></textarea>
      </div>
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
  flex-direction: column;
  align-items: center;
  width: 400px;
  height: 300px;
  padding: 20px;
  background-color: #fdfdfd;
  border-radius: 20px;
  box-shadow: 1px 7px 14px 3px rgba(0, 0, 0, 0.25);

  .title {
    font-size: 18px;
    margin-bottom: 20px;
  }

  .level-box {
    width: 80%;
    display: flex;
    justify-content: space-between;
    margin-bottom: 20px;

    .level {
      padding: 5px;
      border-radius: 10px;
      cursor: pointer;
    }

    .level1 {
      border: 1px solid #3cde02;
      color: #3cde02;
    }
    .level1.select {
      background-color: #3cde0233;
    }
    .level2 {
      border: 1px solid #4dd6d3;
      color: #4dd6d3;
    }
    .level2.select {
      background-color: #4dd6d333;
    }
    .level3 {
      border: 1px solid #62a9f7;
      color: #62a9f7;
    }
    .level3.select {
      background-color: #62a9f733;
    }
    .level4 {
      border: 1px solid #2779f6;
      color: #2779f6;
    }
    .level4.select {
      background-color: #2779f633;
    }
    .level5 {
      border: 1px solid #2350d9;
      color: #2350d9;
    }
    .level5.select {
      background-color: #2350d933;
    }
  }

  .close-btn {
    position: absolute;
    right: 25px;
    top: 25px;
    background-color: #fff;
    transition: 0.3s;

    &:hover {
      padding: 10px;
      background-color: #eee;
      transform: translate(5px, -5px);
    }
  }

  .text-area {
    display: flex;
    justify-content: center;
    align-items: center;
    width: 80%;
    height: 120px;
    border-radius: 10px;
    padding: 10px;
    box-shadow: 1px 2px 15px 0px rgba(0, 0, 0, 0.1) inset;

    textarea {
      width: 100%;
      height: 100%;
      background-color: transparent;
      font-size: 1.2rem;
      font-family: 'GmarketSans';
    }
    textarea::placeholder {
      padding-top: 40px;
      text-align: center;
    }
  }
}
</style>
