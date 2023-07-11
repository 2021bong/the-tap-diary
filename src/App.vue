<script lang="ts">
import { defineComponent } from 'vue';
import Month from './components/Month.vue';

import { initializeApp } from 'firebase/app';
import { getAnalytics } from 'firebase/analytics';
import {
  getFirestore,
  collection,
  getDocs,
  Firestore,
} from 'firebase/firestore/lite';
import dayjs from 'dayjs';

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
  setup() {},
});
</script>

<template>
  <div>
    <button class="korean_lan btn">한국어</button>
    <button class="english_lan btn">English</button>
    <h1 class="title">맨날 우는 사람이 우는 이유</h1>
    <p class="desc">오늘은 또 무슨 이유로 울었을까요? 🥲</p>
  </div>
  <Month />
</template>

<style scoped lang="scss">
.btn {
  width: 100px;

  &:first-of-type {
    margin-right: 10px;
  }
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
