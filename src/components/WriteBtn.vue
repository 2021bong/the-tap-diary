<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({});
</script>

<template>
  <button class="write-btn">
    <span
      class="pi pi-pencil icon"
      style="font-size: 1.2rem; color: #fff"
    ></span>
  </button>
</template>

<style lang="scss">
.write-btn {
  position: absolute;
  right: 30px;
  bottom: 200px;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 50px;
  height: 50px;
  border: none;
  border-radius: 99%;
  background-color: #2779f6;

  &:hover {
    background-color: #05cef4;
  }

  &:active {
    background-color: #2779f6;
  }
}
</style>
