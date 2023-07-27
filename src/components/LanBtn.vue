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
  <button>
    {{ lanType }}
  </button>
</template>

<style lang="scss"></style>
