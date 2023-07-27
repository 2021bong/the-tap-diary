<script lang="ts">
import { defineComponent, reactive } from 'vue';
import Month from '../components/Month.vue';
import LanBtn from '../components/LanBtn.vue';
import WriteBtn from '../components/WriteBtn.vue';

export default defineComponent({
  setup() {
    const data = reactive({
      activeKr: true,
    });

    const changeButtonState = (e: Event) => {
      const target = e.target as HTMLButtonElement;
      target.id === 'kr' ? (data.activeKr = true) : (data.activeKr = false);
    };

    return { data, changeButtonState };
  },
  components: {
    Month,
    LanBtn,
    WriteBtn,
  },
});
</script>

<template>
  <div class="container">
    <button
      id="kr"
      class="lan-btn"
      :class="data.activeKr ? 'select' : null"
      @click="changeButtonState"
    >
      한국어
    </button>
    <button
      id="en"
      class="lan-btn"
      :class="!data.activeKr ? 'select' : null"
      @click="changeButtonState"
    >
      English
    </button>
    <div>
      <h1 class="title">맨날 우는 사람이 우는 이유</h1>
      <p class="desc">오늘은 또 무슨 이유로 울었을까요? 🥲</p>
    </div>
    <Month />
    <WriteBtn />
  </div>
</template>

<style scoped lang="scss">
.container {
  position: relative;
  max-width: 600px;
  margin: 0 auto;
  padding: 2rem;
  text-align: center;
}
.lan-btn {
  width: 100px;

  &:first-of-type {
    margin-right: 10px;
  }
}

.lan-btn.select {
  background-color: #e2e2e2;
}
.title {
  margin: 10px 0;
  font-weight: 800;
}

.desc {
  display: inline-block;
  margin-bottom: 20px;
  padding: 5px 20px;
  background-color: #dfe9f5;
  border-radius: 16px;
}
</style>
