<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
  props: {
    date: String,
    level: Number,
    reason: String,
    reasonEn: String,
    activeKr: Boolean,
  },
});
</script>

<template>
  <li class="item-box">
    <div class="level-box" :class="'level' + level">Lv {{ level }}</div>
    <div class="content-box">
      <p class="reason">
        {{ activeKr ? reason : reasonEn }}
      </p>
      <p class="date">
        {{ date }}
      </p>
    </div>
  </li>
</template>

<style lang="scss">
.item-box {
  display: flex;
  width: 90%;
  margin-top: 15px;
  padding-bottom: 15px;
  border-bottom: 1px solid #e9e9e9;

  &:first-child {
    margin-top: 0;
  }

  &:last-of-type {
    border: none;
  }

  .level-box {
    display: flex;
    justify-content: center;
    align-items: center;
    width: 45px;
    height: 24px;
    margin: 4px 18px 0 0;
    padding: 5px;
    border-radius: 10px;
    cursor: pointer;
  }

  .level1 {
    border: 1px solid #3cde02;
    color: #3cde02;
    background-color: #3cde0233;
  }
  .level2 {
    border: 1px solid #4dd6d3;
    color: #4dd6d3;
    background-color: #4dd6d333;
  }
  .level3 {
    border: 1px solid #62a9f7;
    color: #62a9f7;
    background-color: #62a9f733;
  }
  .level4 {
    border: 1px solid #2779f6;
    color: #2779f6;
    background-color: #2779f633;
  }
  .level5 {
    border: 1px solid #2350d9;
    color: #2350d9;
    background-color: #2350d933;
  }

  .content-box {
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    max-width: 85%;

    .reason {
      margin-bottom: 5px;
      text-align: left;
    }
    .date {
      color: #999;
      font-size: 12px;
    }
  }
}
</style>
