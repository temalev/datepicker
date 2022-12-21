<template>
<div class="main">
  <header>
    <button @click="ClickLastMonth"> &lt; </button>
    <span class="title">{{ currentMonthName }} {{ howYear }}</span>
    <button @click="ClickNextMonth"> &gt; </button>
  </header>

  <div class="body">
    <div class="daysOfWeek">
      <div v-for="dayOfWeek in daysString" :key="dayOfWeek" class="dayOfWeek">
        {{ dayOfWeek }}
      </div>
    </div>
    <div class="daysContainer">
      <div v-for="dayNull in dayWeek" :key="dayNull" class="day null"></div>

      <div v-for="day in lastDayMonth"
          :key="day.timestamp"
          class="day"
          :class="chooseDay === day.timestamp 
          ? 'choose' 
          : 'day'"
          @click="chooseDay = chooseDay != day.timestamp ? day.timestamp : null "
          >
          {{ day.name }}
      </div>
    </div>
  </div>
</div>
</template>
<script>
export default {
  name: 'Calendar',

  data(){
    return {
      daysString: ["пн", "вт", "ср", "чт", "пт", "сб", "вс"],
      currentMonth: new Date().getMonth(),
      currentYear: new Date().getFullYear(),
      currentMonthNow: new Date().getMonth(),
      currentYearNow: new Date().getFullYear(),
      currentDay: new Date().getDate(),
      YearNow: new Date().getFullYear(),
      currentYearNext: new Date().getFullYear()+1,
      chooseDay: 1669928400000,
      events: []
    }
  },

  computed: {
    currentMonthName(){
      return new Date(this.currentYear, this.currentMonth).toLocaleString("default", {month: "long"})
    },

    howYear(){
      if (this.nextMonthInt === 0) return this.currentYear
      else return this.currentYear
    },

    currentMonthNameInt(){
        return new Date(this.currentYear, this.currentMonth).getMonth()
      },

    nextMonthInt(){
        return new Date(this.currentYear, this.currentMonth+1,1).getMonth()
      },

    lastDayMonth(){
      const count = new Date(this.currentYear, this.currentMonth+1, 0).getDate()
      const arr = []

      for (let i = 1; i <= count; i++) {
        arr.push({
          name: i,
          timestamp: new Date(this.currentYear, this.currentMonth, i + 1).getTime()
        })
      }
      return arr
    },

    dayWeek(){
      return new Date(this.currentYear, this.currentMonth, 0).getDay()
    }
  },
  methods: {
    ClickNextMonth (){
        this.currentMonth++

        if (this.currentMonth === 12) {
          this.currentYear++
          this.currentMonth = 0}
    },
      ClickLastMonth (){
        this.currentMonth--
        
        if (this.currentMonth === -1) {
          this.currentYear--
          this.currentMonth = 11}
      },
  }
}
</script>

<style scoped>
.main {
  width: 280px;
  border: 1px solid rgb(174, 174, 174);
  border-radius: 5px;
  padding: 0 10px 10px 10px;
  box-shadow: 0px 10px 20px #cfcfcfa2;
}

header {
  height: 30px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px;
}

.daysOfWeek {
  display: flex;
  width: 100%;
  justify-content: flex-start;
  
}

.dayOfWeek {
  width: 40px;
  height: 30px;
}

.daysContainer{
  display: flex;
  justify-content: flex-start;
  flex-wrap: wrap;
}

.day {
  width: 40px;
  height: 40px;
  display: flex;
  justify-content: center;
  align-items: center;
  cursor: pointer;
  border-radius: 5px;
}

.day:hover {
  outline: 1px solid rgba(156, 156, 156, 0.661);
}

.null {
  outline: none !important;
  cursor: default;
}

button {
  background: none;
  border: none;
  cursor: pointer;
  opacity: .5;
  transition: .2s;
}

button:hover {
  opacity: 1;
}

.choose{
  background-color: rgba(34, 113, 24, 0.824);
  color: #f6f6f6;
  box-shadow: inset 0 0 5px rgba(23, 76, 16, 0.824);
}
</style>