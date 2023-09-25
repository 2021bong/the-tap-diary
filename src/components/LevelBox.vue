<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'LevelBox',
  props: {
    activeKr: Boolean,
  },
});
</script>

<template>
  <div class="wrap">
    <div class="triangle"></div>
    <div class="info-container">
      <h5 class="info-title">
        {{ activeKr ? '눈물 레벨' : 'Tear Level' }}
      </h5>
      <p class="desc">
        {{
          activeKr
            ? '얼마나 많이 울었는지 눈물의 양에 대한 레벨입니다.'
            : "It's the level of the amount of tears."
        }}
      </p>
      <ul>
        <li class="level-box">
          <span class="level level1">Lv1</span>
          <span class="level-name">{{ activeKr ? '울컥' : 'touched' }}</span>
        </li>
        <li class="level-box">
          <span class="level level2">Lv2</span>
          <span class="level-name">{{ activeKr ? '글썽' : 'teary eyes' }}</span>
        </li>
        <li class="level-box">
          <span class="level level3">Lv3</span>
          <span class="level-name">{{ activeKr ? '또르륵' : 'weep' }}</span>
        </li>
        <li class="level-box">
          <span class="level level4">Lv4</span>
          <span class="level-name">{{ activeKr ? '주륵주륵' : 'sob' }}</span>
        </li>
        <li class="level-box">
          <span class="level level5">Lv5</span>
          <span class="level-name">{{ activeKr ? '꺼이꺼이' : 'wail' }}</span>
        </li>
      </ul>
      <p class="information">
        {{
          activeKr
            ? `* 월을 클릭하면 다른 달의 데이터도 볼 수 있어요!`
            : '* If you click month, you can see other month data!'
        }}
      </p>
    </div>
  </div>
</template>

<style lang="scss" scoped>
.wrap {
  position: absolute;
  left: 50px;
  top: -20px;
  font-family: 'GmarketSans';

  .info-container {
    padding: 15px 18px;
    width: 200px;
    background: #fff;
    border-radius: 20px;
    box-shadow: 2px 7px 14px 3px rgba(0, 0, 0, 0.15);
    z-index: 1;

    .info-title {
      margin-bottom: 15px;
      color: #333;
      font-size: 1.2rem;
    }

    .desc {
      margin-bottom: 10px;
      text-align: left;
      font-size: 12px;
      line-height: 1.24;
      color: #555;
    }

    .level-box {
      width: 80%;
      display: flex;
      align-items: center;
      margin-bottom: 10px;
      font-size: 12px;

      .level-name {
        color: #333;
        font-size: 12px;
      }

      .level {
        width: 3em;
        margin-right: 10px;
        padding: 5px;
        border-radius: 10px;
        font-size: 12px;
        cursor: pointer;
      }

      .level1 {
        border: 1px solid #3cde02;
        background-color: #3cde0233;
        color: #3cde02;
      }
      .level2 {
        border: 1px solid #4dd6d3;
        background-color: #4dd6d333;
        color: #4dd6d3;
      }
      .level3 {
        border: 1px solid #62a9f7;
        background-color: #62a9f733;
        color: #62a9f7;
      }
      .level4 {
        border: 1px solid #2779f6;
        background-color: #2779f633;
        color: #2779f6;
      }
      .level5 {
        border: 1px solid #2350d9;
        background-color: #2350d933;
        color: #2350d9;
      }
    }
    .information {
      font-size: 12px;
      line-height: 1.24;
    }
  }
  .triangle {
    position: absolute;
    left: -5px;
    top: 30px;
    width: 20px;
    height: 20px;
    background-color: #fff;
    box-shadow: 1px 1px 17px 5px rgba(0, 0, 0, 0.1);

    transform: skewX(50deg);
    z-index: -1;
  }
}
</style>
