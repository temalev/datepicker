<template>
  <div class="mainContainer">
    <div class="form">
      <div class="inputContainer">
        <span class="title">Название события</span>
        <input
          placeholder="День рождение Бобика"
          v-model="inputEvent"
          class="inputEvent"
          type="text"
        />
      </div>

      <div class="inputContainer">
        <span class="title">Выберите дату</span>
        <div class="wrapper">
          <input
            placeholder="02.02.2023"
            class="inputDate"
            type="text"
            v-model="model"
            readOnly="true"
          />
          <div @click="isCalendar = !isCalendar" class="btnCalendar" />
          <calendar v-if="isCalendar" :events="events" @chooseDay="chooseDay" />
        </div>
      </div>
      <button @click="addEvent" class="btnEvent">Добавить событие</button>
    </div>
  </div>
</template>

<script>
import calendar from "./calendar.vue";

export default {
  components: { calendar },
  name: "DataPicker",

  data() {
    return {
      inputEvent: "",
      model: "",
      isCalendar: false,
      events: [
        {
          info: "День Святого Валентина",
          day: 1676322000000,
        },
        {
          info: "День Победы",
          day: 1683579600000,
        },
        {
          info: "Международный женский день",
          day: 1678222800000,
        },
        {
          info: "Рождество Христово",
          day: 1673038800000,
        },
        {
          info: "День весны и труда",
          day: 1682888400000,
        },
        {
          info: "День народного единства",
          day: 1699045200000,
        },
        {
          info: "День России",
          day: 1686517200000,
        },
      ],
      chooseDayTimestamp: null,
    };
  },

  methods: {
    addEvent() {
      if (this.inputEvent) {
        const newEvent = {
          info: this.inputEvent,
          day: this.chooseDayTimestamp,
        };
        this.events.push(newEvent);
      }
      console.log(this.events);

      this.inputEvent = null;
      this.model = null;
    },
    chooseDay(val) {
      this.model = val?.dateFormatted;
      this.chooseDayTimestamp = val?.timestamp;
    },
  },
};
</script>

<style scoped>
.mainContainer {
  position: relative;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  gap: 10px;
  width: 100%;
}

.form {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  gap: 15px;
  width: 80%;
}

.inputContainer {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  gap: 5px;
  width: 500px;
}

.wrapper {
  cursor: pointer;
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
  cursor: pointer;
  border: none;
  outline: none;
  font-size: 18px;
  width: 100px;
}

.inputEvent {
  border: 1px solid rgba(206, 206, 206, 0.757);
  border-radius: 5px;
  padding: 10px;
  outline: none;
  font-size: 18px;
  width: 100%;
  box-sizing: border-box;
}

.btnCalendar {
  background-image: url(@/ico/icons8-calendar-24.png);
  background-repeat: no-repeat;
  background-position: center;
  width: 20px;
  height: 20px;
  opacity: 0.8;
  cursor: pointer;
  transition: 0.2s;
}

.btnCalendar:hover {
  opacity: 1;
}

.btnEvent {
  background-color: rgb(68, 145, 62);
  color: #fafafa;
  border: 1px solid rgba(206, 206, 206, 0.757);
  border-radius: 10px;
  padding: 10px 15px;
  cursor: pointer;
  transition: 0.2s;
}

.btnEvent:hover {
  box-shadow: 0 2px 5px rgba(38, 81, 35, 0.435);
  border: 1px solid rgba(111, 111, 111, 0.757);
}

@media (max-width: 700px) {
  .inputContainer {
    width: 100%;
  }
}
</style>
