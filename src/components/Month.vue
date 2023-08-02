<script lang="ts">
import { defineComponent, reactive } from 'vue';

export default defineComponent({
  props: {
    lan: Boolean,
  },
  setup() {
    const data = reactive({
      monthKr: new Date().getMonth() + 1 + '월',
      monthEn: 'Aug',
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
  padding: 10px 20px;
  background-color: #80a6ff;
  border: none;
  border-radius: 16px;
  color: #fff;
  font-size: 1.2rem;
  font-weight: 700;
}
</style>
