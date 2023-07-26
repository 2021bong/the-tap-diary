<script lang="ts">
import { defineComponent, reactive } from 'vue';

interface ComponentData {
  monthArr: (string | number)[];
}

export default defineComponent({
  setup() {
    const data: ComponentData = reactive({
      monthArr: ['7월'],
    });

    return {
      data,
    };
  },
});
</script>

<template>
  <div class="button">{{ data.monthArr[0] }}</div>
</template>

<style scoped lang="scss">
.button {
  display: inline-block;
  padding: 10px 20px;
  background-color: #80a6ff;
  border: none;
  border-radius: 16px;
  color: #fff;
  font-weight: 700;
}
</style>
