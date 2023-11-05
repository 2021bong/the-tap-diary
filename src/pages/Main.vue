<script lang="ts">
import { defineComponent, reactive } from 'vue';
import Month from '../components/Month.vue';
import LanBtn from '../components/LanBtn.vue';
import DiaryItem from '../components/DiaryItem.vue';
import LevelBox from '../components/LevelBox.vue';
import DiaryItemType from '../types/diaryItemType';
import DateModal from './DateModal.vue';
import axios from 'axios';

export default defineComponent({
  name: 'Main',
  components: {
    Month,
    LanBtn,
    DiaryItem,
    LevelBox,
    DateModal,
  },
  props: {
    diarys: Array as () => DiaryItemType[],
    thisMonth: String,
  },
  emits: ['change-diarys'],
  setup(props, { emit }) {
    const data = reactive({
      activeKr: true,
      showLevel: false,
      showModal: false,
      isLoading: false,
    });

    const changeButtonState = (e: Event) => {
      const target = e.target as HTMLButtonElement;
      target.id === 'kr' ? (data.activeKr = true) : (data.activeKr = false);
      if (!data.activeKr) {
        if (!props.diarys?.[0].reasonEn) {
          data.isLoading = true;
          const krText = props.diarys?.map((item) => item.reason);
          axios
            .post(import.meta.env.VITE_TRANSLATE_URL, { text: krText })
            .then((res) => {
              const enText = res.data;
              props.diarys?.map((item, i) => (item.reasonEn = enText[i]));
            })
            .then(() => (data.isLoading = false));
        } else {
          console.log('There was reasonEn');
          data.isLoading = false;
        }
      }
    };

    const showLevelBoxForPc = (e: Event) => {
      e.type === 'mouseenter'
        ? (data.showLevel = true)
        : (data.showLevel = false);
    };
    const showLevelBoxMobile = (e: Event) => {
      const target = e.target as HTMLElement;
      target.id === 'levelInfo'
        ? (data.showLevel = true)
        : (data.showLevel = false);
    };

    const showDateModal = () => {
      data.showModal = !data.showModal;
    };

    const changeDairys = (data: string) => {
      emit('change-diarys', data);
    };

    return {
      data,
      changeButtonState,
      showDateModal,
      showLevelBoxForPc,
      showLevelBoxMobile,
      changeDairys,
    };
  },
});
</script>

<template>
  <div class="container" @click="showLevelBoxMobile">
    <template v-if="data.isLoading">
      <div class="background">
        <i
          class="pi pi-spin pi-spinner"
          style="font-size: 2rem; color: #fff"
        ></i>
      </div>
    </template>
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
    <header>
      <h1 class="title">{{ data.activeKr ? '수도꼭지 일기' : 'TAP DIARY' }}</h1>
      <p class="desc">
        {{
          data.activeKr
            ? '수도꼭지는 왜 열렸을까 ? 🥲'
            : 'Why did the tap open ? 🥲'
        }}
      </p>
    </header>
    <main class="main">
      <span
        id="levelInfo"
        class="pi pi-question-circle question"
        style="font-size: 1.7rem; color: #aaa"
        @mouseenter="showLevelBoxForPc"
        @mouseleave="showLevelBoxForPc"
      >
        <LevelBox v-show="data.showLevel" :activeKr="data.activeKr" />
      </span>
      <Month
        id="monthBtn"
        :month="thisMonth"
        :lan="data.activeKr"
        @click="showDateModal"
      />
      <div v-if="diarys?.length === 0" class="no-data">
        이달은 울지 않았어요! 👏👏👏
      </div>
      <ul v-else class="diary">
        <DiaryItem
          v-for="item in diarys"
          :key="item.date"
          :level="item.level"
          :date="item.date"
          :reason="item.reason"
          :reasonEn="item.reasonEn"
          :activeKr="data.activeKr"
        />
      </ul>
    </main>
  </div>
  <DateModal
    v-if="data.showModal"
    :lan="data.activeKr"
    @show-modal="showDateModal"
    @change-diarys="changeDairys"
  />
</template>

<style scoped lang="scss">
.container {
  position: relative;
  max-width: 600px;
  margin: 0 auto;
  height: 100vh;
  padding: 2rem;
  text-align: center;
}

.background {
  position: absolute;
  left: 0;
  top: 0;
  display: flex;
  justify-content: center;
  align-items: flex-start;
  padding-top: 200px;
  width: 100%;
  height: 100%;
  background-color: rgba(100, 100, 100, 0.6);
  z-index: 1;
}
.lan-btn {
  width: 100px;
  padding: 15px 5px;
  border: 1px solid #eee;
  background-color: #fff;
  font-size: 1em;
  font-weight: 500;
  font-family: inherit;
  transition: border-color 0.25s;

  &:first-of-type {
    margin-right: 10px;
  }
}

.lan-btn.select {
  background-color: #e2e2e2;
}
.title {
  margin: 20px 0 5px 0;
  font-weight: 800;
}

.desc {
  display: inline-block;
  margin-bottom: 30px;
  padding: 5px 20px;
  background-color: #dfe9f5;
  border-radius: 16px;
}

.main {
  position: relative;

  .no-data {
    width: 60%;
    min-width: 275px;
    height: 100px;
    margin: 30px auto 0 auto;
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: #fffedf;
    border-radius: 10px;
  }

  .diary {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }

  .question {
    position: absolute;
    left: 0.5rem;
    top: 0;
    display: inline-block;
  }
}
</style>
