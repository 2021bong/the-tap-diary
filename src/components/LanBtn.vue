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
  <button class="lan-btn" :class="select ? 'select' : null">
    {{ lanType }}
  </button>
</template>

<style lang="scss">
.lan-btn {
  width: 100px;

  &:first-of-type {
    margin-right: 10px;
  }
}

.lan-btn.select {
  background-color: #e2e2e2;
}
</style>
