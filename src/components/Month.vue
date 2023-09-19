<script lang="ts">
import { defineComponent, reactive } from 'vue';
import MonthsType from '../types/monthsType'

const monthsEn : MonthsType = {
  '1':'Jan',
  '2':'Fab',
  '3':'Mar',
  '4':'Apr',
  '5':'May',
  '6':'Jun',
  '7':'Jul',
  '8':'Aug',
  '9':'Sept',
  '10':'Oct',
  '11':'Nov',
  '12':'Dec',
}
const thisMonth = (new Date().getMonth() + 1).toString();

export default defineComponent({
  props: {
    lan: Boolean,
  },
  setup() {
    const data = reactive({
      monthKr: thisMonth + '월',
      monthEn: monthsEn[thisMonth as keyof MonthsType],
    });

    return {
      data,
    };
  },
});
</script>

<template>
  <button class="button">
    {{ lan ? data.monthKr : data.monthEn }}
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
}
</style>
