<script lang="ts">
import { defineComponent, ref } from 'vue';
import MonthsType from '../types/monthsType';

const MONTH_EN: MonthsType = {
  '1': 'Jan',
  '2': 'Fab',
  '3': 'Mar',
  '4': 'Apr',
  '5': 'May',
  '6': 'Jun',
  '7': 'Jul',
  '8': 'Aug',
  '9': 'Sep',
  '10': 'Oct',
  '11': 'Nov',
  '12': 'Dec',
};

export default defineComponent({
  props: {
    lan: Boolean,
    month: String,
  },
  setup() {
    const monthEN = ref(MONTH_EN);

    return {
      monthEN,
    };
  },
});
</script>

<template>
  <button class="button">
    {{ lan ? month + '월' : monthEN[month as keyof MonthsType] }}
  </button>
</template>

<style scoped lang="scss">
.button {
  display: inline-block;
  margin-bottom: 15px;
  padding: 10px 20px;
  background-color: #80a6ff;
  border: none;
  border-radius: 16px;
  color: #fff;
  font-size: 1.2rem;
  font-weight: 700;
  transition: 0.3s all;

  &:active {
    background-color: #2779f6;
  }
}
</style>
