<template>
  <div>
    <div
      v-if="
        day !== 0 &&
          today === day &&
          currentDate.year === year &&
          currentDate.month === month
      "
      class="today-style"
    >
      {{ day }}
    </div>
    <div
      v-if="
        day !== 0 &&
          (currentDate.year !== year ||
            currentDate.month !== month ||
            today !== day)
      "
      class=""
    >
      {{ day }}
    </div>
  </div>
</template>

<script>
export default {
  name: "DayInCalendar",
  props: {
    day: Number,
    today: Number,
    year: Number,
    month: String,
    currentDate: Object,
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.today-style {
  color: red;
}
</style>
