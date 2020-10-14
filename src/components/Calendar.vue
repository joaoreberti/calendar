<template>
  <div class="calendar">
    <div>{{ year }}</div>
    <div class="prev-month-next">
      <div @click="previousMonth">Previous Month</div>

      <div>{{ month }}</div>
      <div @click="nextMonth">Next Month</div>
    </div>

    <div class="week-days">
      <div>Sun</div>
      <div>Mon</div>
      <div>Tue</div>
      <div>Wed</div>
      <div>Thu</div>
      <div>Fri</div>
      <div>Sat</div>
    </div>
    <div class="row">
      <div
        class="day-in-calendar"
        v-for="n in firstDay"
        :key="'empty days' + n"
      >
        <DayInCalendar v-bind:day="0" />
      </div>
      <div class="day-in-calendar" v-for="n in days" :key="n">
        <DayInCalendar
          v-bind:year="year"
          v-bind:month="month"
          v-bind:today="today"
          v-bind:day="n"
          v-bind:currentDate="currentDate"
        />
      </div>
    </div>
  </div>
</template>

<script>
import DayInCalendar from "./DayInCalendar";
export default {
  name: "Calendar",
  components: {
    DayInCalendar,
  },
  props: {
    month: String,
    days: Number,
    firstDay: Number,
    today: Number,
    previousMonth: Function,
    nextMonth: Function,
    year: Number,
    currentDate: Object,
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.calendar {
  display: flex;
  flex-direction: column;
}
.prev-month-next {
  display: flex;
  justify-content: space-around;
  margin-bottom: 2rem;
}

.row {
  display: flex;
  flex-wrap: wrap;
  margin-top: 50px;
  height: 70vh;
  margin: auto;
  margin-top: 1rem;
  width: 100%;
}
.day-in-calendar {
  width: calc(100% / 7);
  height: calc(100% / 6);
}

.day-in-calendar:nth-child(7n) {
  background-color: #42b983;
}

.week-days {
  display: flex;
  margin-top: 50px;
  margin: auto;
  margin-top: 1rem;
  width: 100%;
  margin-bottom: 1rem;
}

.week-days div {
  width: calc(100% / 7);
  background-color: #304455;
  color: whitesmoke;
}
</style>
