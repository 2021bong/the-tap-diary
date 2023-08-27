<script lang="ts">
import { defineComponent, ref } from 'vue';
import Main from './pages/Main.vue';
import WriteModal from './pages/WriteModal.vue';
import DiaryItemType from './types/diaryItemType';

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
  const date = new Date();
  const year = date.getFullYear();
  const month = (date.getMonth() + 1).toString();
  const twoDigitMonth = month.length < 2 ? '0' + month : month;
  const thisMonthData = collection(database, `${year}_${twoDigitMonth}`);
  const monthDataDoc = await getDocs(thisMonthData);
  const monthDatas = monthDataDoc.docs.map((doc) => doc.data());
  return monthDatas;
};

const data = await getData(db);
data.sort((a, b) => {
  return dayjs(a.date).isAfter(dayjs(b.date)) ? -1 : 1;
});
// console.log('data level:', data.level);
// console.log('data date:', dayjs(data.date).format('YYYY-MM-DD hh:mm:ss'));
// console.log('data reason:', data.reason);

export default defineComponent({
  setup() {
    const isShowModal = ref(false);
    const diarys = ref(data as DiaryItemType[]);

    const showModal = () => {
      isShowModal.value = !isShowModal.value;
    };

    return { isShowModal, showModal, diarys };
  },
  components: {
    Main,
    WriteModal,
  },
});
</script>

<template>
  <Main @show-modal="showModal" :diarys="diarys" />
  <div v-if="isShowModal">
    <WriteModal @show-modal="showModal" />
  </div>
</template>

<style lang="scss"></style>
