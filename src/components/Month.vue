<script lang="ts">
import { defineComponent, reactive } from 'vue';

interface ComponentData {
  monthArr: (string | number)[];
}

export default defineComponent({
  setup() {
    const data: ComponentData = reactive({
      monthArr: [],
    });

    return {
      data,
    };
  },
});
</script>

<template>
  <div class="container">6월</div>
</template>

<style scoped lang="scss">
.container {
  display: inline-block;
  padding: 10px 20px;
  background-color: #80a6ff;
  border-radius: 16px;
  color: #fff;
  font-weight: 700;
}
</style>
