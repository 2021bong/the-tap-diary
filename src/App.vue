<script lang="ts">
import { defineComponent, reactive } from 'vue';
import Month from './components/Month.vue';
import WriteBtn from './components/WriteBtn.vue';

import { initializeApp } from 'firebase/app';
import { getAnalytics } from 'firebase/analytics';
import {
  getFirestore,
  collection,
  getDocs,
  Firestore,
} from 'firebase/firestore/lite';
import dayjs from 'dayjs';
import 'primeicons/primeicons.css';

const firebaseConfig = {
  apiKey: import.meta.env.VITE_FIREBASE_APIKEY,
  authDomain: import.meta.env.VITE_FIREBASE_AUTHDOMAIN,
  projectId: import.meta.env.VITE_FIREBASE_PROJECTID,
  storageBucket: import.meta.env.VITE_FIREBASE_STORAGEBUCKET,
  messagingSenderId: import.meta.env.VITE_FIREBASE_MESSAGINGSENDERID,
  appId: import.meta.env.VITE_FIREBASE_APPID,
  measurementId: import.meta.env.VITE_FIREBASE_MEASUREMENTID,
};

const app = initializeApp(firebaseConfig);
getAnalytics(app);
const db = getFirestore(app);

const getData = async (database: Firestore) => {
  const thisMonthData = collection(database, '2023_07');
  const monthDataDoc = await getDocs(thisMonthData);
  const monthDatas = monthDataDoc.docs.map((doc) => doc.data());
  return monthDatas;
};

const data = await getData(db);
data.forEach((data) => {
  console.log('data level:', data.level);
  console.log('data date:', dayjs(data.date).format('YYYY-MM-DD hh:mm:ss'));
  console.log('data reason:', data.reason);
});

export default defineComponent({
  setup() {
    const data = reactive({
      selectedKr: true,
    });

    const changeButtonState = (e: Event) => {
      const target = e.target as HTMLButtonElement;
      target.id === 'kr' ? (data.selectedKr = true) : (data.selectedKr = false);
    };

    return { data, changeButtonState };
  },
  components: {
    Month,
    WriteBtn,
  },
});
</script>

<template>
  <div>
    <button
      id="kr"
      class="korean_lan btn"
      :class="data.selectedKr ? 'select' : null"
      @click="changeButtonState"
    >
      한국어
    </button>
    <button
      id="en"
      class="english_lan btn"
      :class="!data.selectedKr ? 'select' : null"
      @click="changeButtonState"
    >
      English
    </button>
    <h1 class="title">맨날 우는 사람이 우는 이유</h1>
    <p class="desc">오늘은 또 무슨 이유로 울었을까요? 🥲</p>
  </div>
  <Month />
  <WriteBtn />
</template>

<style scoped lang="scss">
.main-container {
  display: relative;
}
.btn {
  width: 100px;

  &:first-of-type {
    margin-right: 10px;
  }
}

.btn.select {
  background-color: #e2e2e2;
}

.title {
  margin: 10px 0;
  font-weight: 800;
}

.desc {
  display: inline-block;
  margin-bottom: 10px;
  padding: 5px 20px;
  background-color: #dfe9f5;
  border-radius: 16px;
}
</style>
