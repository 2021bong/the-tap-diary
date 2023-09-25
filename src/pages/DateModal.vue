<script lang="ts">
import { defineComponent, ref } from 'vue';

const START_YEAR = 2023;
const START_MONTH = 7;
const today = new Date();
const thisYear = today.getFullYear();
const thisMonth = today.getMonth() + 1;
const months: string[] = [];
let countDate = `${START_YEAR}_${START_MONTH}`;
while (countDate !== `${thisYear}_${thisMonth}`) {
  months.unshift(countDate);
  let [y, m] = countDate.split('_').map((str) => +str);
  if (+m === 12) {
    y += 1;
    m = 1;
  } else {
    m += 1;
  }
  countDate = `${y}_${m}`;
}
months.unshift(countDate);

export default defineComponent({
  name: 'DateModal',
  emits: ['show-modal'],
  props: {
    lan: Boolean,
  },
  setup(_, { emit }) {
    const selectableMonths = ref(months as string[]);
    const clickHideModalBtn = () => {
      emit('show-modal');
    };

    return { selectableMonths, clickHideModalBtn };
  },
});
</script>

<template>
  <div class="background">
    <div class="date-modal">
      <h4 class="title">월별로 보기</h4>
      <div class="month-box">
        <span
          class="month-badge"
          :class="date.split('_')[1] === '12' ? 'new-year' : ''"
          v-for="date in selectableMonths"
          >{{ date.split('_')[0] + '년' + date.split('_')[1] + '월' }}</span
        >
      </div>
      <button class="close-btn" @click="clickHideModalBtn">
        <span
          class="pi pi-times icon"
          style="font-size: 1.2rem; color: #000"
        ></span>
      </button>
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

  .month-box {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
    width: 100%;
    height: 70%;
    margin-bottom: 30px;
    overflow: scroll;

    .month-badge {
      display: inline-flex;
      justify-content: center;
      align-items: center;
      width: 30%;
      height: 40px;
      margin-bottom: 10px;
      border-radius: 10px;
      color: #80a6ff;
      border: 1px solid #80a6ff;
      transition: 0.3s all;
      cursor: pointer;

      &:hover {
        color: #fff;
        background-color: #80a6ff;
      }
    }

    .month-badge.new-year {
      color: #2350d9;
      border: 1px solid #2350d9;

      &:hover {
        color: #fff;
        background-color: #2350d9;
      }
    }
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
