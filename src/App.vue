<template>
  <div id="app">
    <Calendar
      v-bind:previousMonth="previousMonth"
      v-bind:nextMonth="nextMonth"
      v-bind:month="today.month"
      v-bind:days="today.hasManyDays"
      v-bind:firstDay="today.firstDayOfTheMonth"
      v-bind:today="today.day"
      v-bind:year="today.year"
      v-bind:currentDate="currentDate"
    />
  </div>
</template>

<script>
import Calendar from "./components/Calendar";
export default {
  name: "App",
  components: {
    Calendar,
  },
  computed: {},
  methods: {
    previousMonth: function() {
      this.today = this.getInfo("previousMonth", this.today);
    },
    nextMonth: function() {
      this.today = this.getInfo("nextMonth", this.today);
    },
    getInfo: function(instruction, current) {
      if (instruction && current) {
        if (instruction === "previousMonth") {
          let months = [
            "January",
            "February",
            "March",
            "April",
            "May",
            "June",
            "July",
            "August",
            "September",
            "October",
            "November",
            "December",
          ];
          for (let i = 0; i < months.length; i++) {
            if (current.month === months[i]) {
              console.log("next month ", months[i - 1]);
              console.log("current month");
              if (i === 0) {
                current.year = current.year - 1;
                current.month = months[months.length - 1];
              } else {
                current.month = months[i - 1];
              }
            }
          }

          let dt = new Date(
            current.month + " " + current.day + ", " + current.year
          );

          let dateObject = {};

          let hasManyDays = [31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31];

          dateObject.year = dt.getFullYear();
          dateObject.month = months[dt.getMonth()];
          dateObject.day = dt.getDate();
          dateObject.hasManyDays = hasManyDays[dt.getMonth()];

          let dateForFirstDayOfTheMonth = new Date(
            dateObject.month + " 1, " + dateObject.year
          );
          let firstDayOfTheMonth = dateForFirstDayOfTheMonth.getDay();

          dateObject.firstDayOfTheMonth = firstDayOfTheMonth;

          return dateObject;
        } else if (instruction === "nextMonth") {
          let months = [
            "January",
            "February",
            "March",
            "April",
            "May",
            "June",
            "July",
            "August",
            "September",
            "October",
            "November",
            "December",
          ];

          let helper = "";
          for (let i = 0; i < months.length; i++) {
            if (current.month === months[i]) {
              console.log("next month ", months[i + 1]);
              console.log("i ", i);

              if (i === months.length - 1) {
                current.year = current.year + 1;
                helper = months[0];
              } else {
                helper = months[i + 1];
              }
            }
          }
          current.month = helper;

          let dt = new Date(
            current.month + " " + current.day + ", " + current.year
          );

          let dateObject = {};

          let hasManyDays = [31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31];

          dateObject.year = dt.getFullYear();
          dateObject.month = months[dt.getMonth()];
          dateObject.day = dt.getDate();
          dateObject.hasManyDays = hasManyDays[dt.getMonth()];

          let dateForFirstDayOfTheMonth = new Date(
            dateObject.month + " 1, " + dateObject.year
          );
          let firstDayOfTheMonth = dateForFirstDayOfTheMonth.getDay();

          dateObject.firstDayOfTheMonth = firstDayOfTheMonth;

          return dateObject;
        }
      } else {
        let dt = new Date();
        let dateObject = {};
        let months = [
          "January",
          "February",
          "March",
          "April",
          "May",
          "June",
          "July",
          "August",
          "September",
          "October",
          "November",
          "December",
        ];

        let hasManyDays = [31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31];

        dateObject.year = dt.getFullYear();
        dateObject.month = months[dt.getMonth()];
        dateObject.day = dt.getDate();
        dateObject.hasManyDays = hasManyDays[dt.getMonth()];

        let dateForFirstDayOfTheMonth = new Date(
          dateObject.month + " 1, " + dateObject.year
        );
        let firstDayOfTheMonth = dateForFirstDayOfTheMonth.getDay();

        dateObject.firstDayOfTheMonth = firstDayOfTheMonth;

        return dateObject;
      }
    },
  },
  data() {
    return {
      today: this.getInfo(),
      currentDate: this.getInfo(),
    };
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  font-size: 50px;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
