<script lang="ts">
import { defineComponent, ref } from 'vue';
import Main from './pages/Main.vue';
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

const getData = async () => {
  const date = new Date();
  const year = date.getFullYear();
  const month = (date.getMonth() + 1).toString();
  const twoDigitMonth = month.length < 2 ? '0' + month : month;
  const thisMonthData = collection(db, `${year}_${twoDigitMonth}`);
  const monthDataDoc = await getDocs(thisMonthData);
  const monthDatas = monthDataDoc.docs.map((doc) => doc.data());
  return monthDatas;
};

const data = await getData();
data.sort((a, b) => {
  return dayjs(a.date).isAfter(dayjs(b.date)) ? -1 : 1;
});
// console.log('data level:', data.level);
// console.log('data date:', dayjs(data.date).format('YYYY-MM-DD hh:mm:ss'));
// console.log('data reason:', data.reason);

const month = (new Date().getMonth() + 1).toString();

export default defineComponent({
  setup() {
    const isShowPopup = ref(false);
    let diarys = ref(data as DiaryItemType[]);
    const thisMonth = ref(month);

    const showPopup = () => {
      isShowPopup.value = !isShowPopup.value;
    };

    const changeMonth = async (date: string) => {
      const getNewData = async (database: Firestore) => {
        const thisMonthData = collection(database, date);
        const monthDataDoc = await getDocs(thisMonthData);
        const monthDatas = monthDataDoc.docs.map((doc) => doc.data());
        return monthDatas;
      };

      const data = await getNewData(db);
      const newData = data.sort((a, b) => {
        return dayjs(a.date).isAfter(dayjs(b.date)) ? -1 : 1;
      });
      diarys.value = newData as DiaryItemType[];
      const [_, getM] = date.split('_');
      const noZeroM = Number(getM).toString();
      thisMonth.value = noZeroM;
    };

    const modifyDiarys = (newDiary: DiaryItemType[]) => {
      diarys.value = newDiary;
    };

    return {
      thisMonth,
      isShowPopup,
      showPopup,
      diarys,
      changeMonth,
      modifyDiarys,
    };
  },
  components: {
    Main,
  },
});
</script>

<template>
  <Main
    :diarys="diarys"
    :thisMonth="thisMonth"
    @change-month="changeMonth"
    @modify-diarys="modifyDiarys"
  />
</template>

<style lang="scss"></style>
