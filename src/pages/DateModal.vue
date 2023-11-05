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
  emits: ['show-modal', 'change-month'],
  props: {
    lan: Boolean,
  },
  setup(_, { emit }) {
    const selectableMonths = ref(months as string[]);
    const clickHideModalBtn = (e: Event) => {
      const target = e.target as HTMLElement;
      if (
        target.id === 'modalBg' ||
        target.id === 'closeBtn' ||
        target.id === 'closeIcon'
      ) {
        emit('show-modal');
      }
    };
    const clickDate = (e: Event) => {
      const target = e.target as HTMLDivElement;
      let [pickedY, pickedM] = target.id.split('_');
      if (pickedM.length == 1) {
        pickedM = '0' + pickedM;
      }
      emit('change-month', `${pickedY}_${pickedM}`);
      emit('show-modal');
    };

    return { selectableMonths, clickHideModalBtn, clickDate };
  },
});
</script>

<template>
  <div id="modalBg" class="background modal-bg" @click="clickHideModalBtn">
    <div class="date-modal">
      <h4 class="title">월별로 보기</h4>
      <div class="month-box">
        <span
          class="month-badge"
          :class="date.split('_')[1] === '12' ? 'new-year' : ''"
          :id="date.split('_')[0] + '_' + date.split('_')[1]"
          @click="clickDate"
          v-for="date in selectableMonths"
          >{{ date.split('_')[0] + '년' + date.split('_')[1] + '월' }}</span
        >
      </div>
      <button id="closeBtn" class="close-btn" @click="clickHideModalBtn">
        <span
          id="closeIcon"
          class="pi pi-times icon"
          style="font-size: 1.2rem; color: #000"
        ></span>
      </button>
    </div>
  </div>
</template>

<style lang="scss" scoped>
.modal-bg {
  padding-top: 150px;
  background-color: rgba(100, 100, 100, 0.6);
}
.date-modal {
  position: relative;
  display: flex;
  flex-direction: column;
  max-width: 400px;
  width: 90%;
  margin: 0 auto;
  height: 500px;
  padding: 40px 20px;
  background-color: #fdfdfd;
  border-radius: 20px;
  box-shadow: 1px 7px 14px 3px rgba(0, 0, 0, 0.25);
  box-sizing: border-box;

  .title {
    text-align: center;
    font-size: 18px;
    margin-bottom: 30px;
  }

  .month-box {
    display: flex;
    flex-wrap: wrap;
    width: 100%;
    max-height: 70%;
    margin-bottom: 30px;
    overflow: scroll;

    .month-badge {
      display: flex;
      justify-content: center;
      align-items: center;
      min-width: 108px;
      width: 30%;
      height: 40px;
      margin-right: 10px;
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
