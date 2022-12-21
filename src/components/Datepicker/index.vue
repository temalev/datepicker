<template>

<div class="mainContainer">
  <span class="title">Выберите дату</span>

  <div class="wrapper">
    <input type="tel" v-model="model">
    <div @click="isCalendar = !isCalendar" class="btnCalendar" />
  </div>

  <calendar v-if="isCalendar" />

</div>

</template>

<script>
import calendar from './calendar.vue'

export default {
  components: { calendar },
  name: 'DataPicker',

  data(){
    return {
      
      currentDate: 'dd.mm.yyyy',
      isCalendar: false
    }
  },

  computed:{
    model: {
      get() {
        return this.currentDate
      },
      set(value) {
        this.currentDate = value.replace("-", ".")
      }
    }
  },


}
</script>

<style scoped>
  .mainContainer{
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }

  .wrapper{
    width: 150px;
    border: 1px solid rgba(206, 206, 206, 0.757);
    border-radius: 5px;
    padding: 10px;
    display: flex;
    justify-content: space-around;
  }

  input {
    border: none;
    outline: none;
    font-size: 18px;
    width: 100px;
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
</style>