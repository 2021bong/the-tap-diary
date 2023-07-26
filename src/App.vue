<script lang="ts">
import { defineComponent } from 'vue';
import Main from './pages/Main.vue';
import WriteModal from './pages/WriteModal.vue';

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
  components: {
    Main,
    WriteModal,
  },
});
</script>

<template>
  <Main />
  <!-- <WriteModal /> -->
</template>

<style lang="scss"></style>
