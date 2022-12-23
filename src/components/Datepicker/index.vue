<template>

<div class="mainContainer">
  <span class="title">Выберите дату</span>
  <div class="wrapper">
    <input  class="inputDate" type="text" v-model="model">
    <div @click="isCalendar = !isCalendar" class="btnCalendar" />
    <calendar v-if="isCalendar" :events="events" @chooseDay="chooseDay" />
    
  </div>

  <input v-model="inputEvent" class="inputEvent" type="text">

  <button class="btnEvent">Добавить событие</button>

</div>

</template>

<script>
import calendar from './calendar.vue'

export default {
  components: { calendar },
  name: 'DataPicker',

  data() {
    return {
      inputEvent: '',
      model: '',
      isCalendar: false,
      events: [{
        info: "День Святого Валентина",
        day: '14.02'
      },
      {
        info: "9 Мая",
        day: '09.05'
      }]
    }
  },

  watch: {
    model(value) {
      const rule = value.replace(/[^\d]/g,'')
      this.model = this.formatDateDDMMYYYY(rule)
    }
  },

  methods: {
    chooseDay(val) {
      this.model = val
    },

    formatDateDDMMYYYY(value) {
      const dateFormatMask = "##.##.####"

      let i = 0;
      let lastReplaceIdx = -1;

      const filledMask = dateFormatMask.replace(/#/g, (_, j) => {
        if (i >= value.length) {
      return "#"
      }

      lastReplaceIdx = j;

      return value[i++];
    })

    const [day, month] = filledMask.split(".");

  const d1 = day[0];
  const d2 = day[1];

  if (+day >= 31 && +day <= 39) {
    return filledMask
      .replace(/\d{2}/g, `0${d1}`)
      .replace(/##/g, `0${d2}`)
      .slice(0, 5);
  }

  if (+d1 > 3 && +d1 <= 9) {
    return filledMask.replace(/\d#/g, `0${d1}`).slice(0, 2);
  }

  const m1 = month[0];

  if (+m1 >= 2 && +m1 <= 9) {
    return filledMask.replace(/\d#/g, `0${m1}`).slice(0, 5);
  }


  return filledMask.substring(0, lastReplaceIdx + 1)
    }
  }

  // computed:{
  //   model: {
  //     get() {
  //       return this.currentDate
  //     },
  //     set(value) {
  //       // const cleanValue = value.replace(/[^\d]/g, "")
  //       this.currentDate = value.replace(/[^\d]/gi, "")
  //     }
  //   }
  // },

//   methods: {
//     formatDateDDMMYYYY(value) {
//       const dateFormatMask = "##.##.####"

//       let i = 0;
// let lastReplaceIdx = -1;

//  const filledDateFormatMask = dateFormatMask.replace(/#/g, (_, j) => {
//    if (i >= value.length) {
//    return "#";
//    }

//    lastReplaceIdx = j;

//    return value[i++];
//  })
//  return filledDateFormatMask.substring(0, lastReplaceIdx + 1);

//     }
//   }

}
</script>

<style scoped>
  .mainContainer {
    position: relative;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    gap: 10px;
  }

  .wrapper {
    position: relative;
    width: 150px;
    border: 1px solid rgba(206, 206, 206, 0.757);
    border-radius: 5px;
    padding: 10px;
    display: flex;
    justify-content: space-around;
    align-items: center;
  }

  .inputDate {
    border: none;
    outline: none;
    font-size: 18px;
    width: 100px;
  }

  .inputEvent{
    border: 1px solid rgba(206, 206, 206, 0.757);
    border-radius: 5px;
    padding: 10px;
    outline: none;
    font-size: 18px;
    width: 500px;
  }

  .btnCalendar{
    background-image: url(@/ico/icons8-calendar-24.png);
    background-repeat: no-repeat;
    background-position: center;
    width: 20px;
    height: 20px;
    opacity: .8;
    cursor: pointer;
    transition: .2s;
  }

  .btnCalendar:hover {
    opacity: 1;
  }

  .btnEvent{
    background-color: rgb(68, 145, 62);
    color: #fafafa;
    border: 1px solid rgba(206, 206, 206, 0.757);
    border-radius: 10px;
    padding: 10px 15px;
    cursor: pointer;
    transition: .2s;
  }

  .btnEvent:hover {
    box-shadow: 0 2px 5px rgba(38, 81, 35, 0.435);
    border: 1px solid rgba(111, 111, 111, 0.757);
  }
</style>