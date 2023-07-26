<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
  props: {
    lanType: String,
    select: Boolean,
  },
});
</script>

<template>
  <button class="btn" :class="select ? lanType + ' select' : lanType">
    {{ lanType }}
  </button>
</template>

<style lang="scss">
.btn {
  width: 100px;

  &:first-of-type {
    margin-right: 10px;
  }
}

.btn.select {
  background-color: #e2e2e2;
}
</style>
