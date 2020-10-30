<template>
  <section class="calendar">
    <h2>November 2020</h2>
    <div class="calendar__content">
      <div class="calendar__weekdays">
        <span>Mon</span>
        <span>Tue</span>
        <span>Wed</span>
        <span>Thu</span>
        <span>Fri</span>
        <span>Sat</span>
        <span>Sun</span>
      </div>
      <div class="calendar__days">
        <span
          v-for="day in 30"
          :key="'day' + day"
          :class="[
            {
              'cal-has-task': checkForDayInTodoList(day)[0] == 'task',
              'cal-is-overdue': checkForDayInTodoList(day)[1] == 'overdue',
            },
          ]"
        >
          {{ day }}
        </span>
      </div>
    </div>
  </section>
</template>
<script>
export default {
  name: "Calendar",
  props: { todoList: Array },
  methods: {
    checkForDayInTodoList(day) {
      for (let index in this.todoList) {
        let dueDateDay = this.todoList[index].dueDate.split("-")[2];
        if (day == dueDateDay && !this.todoList[index].isDone) {
          if (this.todoList[index].isOverdue) {
            return ["task", "overdue"];
          } else {
            return ["task"];
          }
        }
      }
      return false;
    },
  },
};
</script>
<style scoped>
.calendar {
  width: 500px;
  text-align: center;
  margin: 75px auto 50px auto;
}

.calendar__content > div {
  display: flex;
  width: 100%;
}

.calendar__weekdays {
  margin-bottom: 10px;
}

.calendar__weekdays > span {
  display: inline-block;
  width: 13%;
  margin-left: 1.125%;
  padding: 5px;
  background-color: olivedrab;
  color: white;
}

.calendar__days {
  flex-wrap: wrap;
}

.calendar__days > span {
  display: inline-block;
  width: 13%;
  padding: 5px;
  margin-left: 1.125%;
  margin-bottom: 1.125%;
  border: 2px solid #ddd;
}

.calendar__days > span:first-of-type {
  margin-left: 85.875%;
}

.calendar__days .cal-has-task {
  border: 2px solid olivedrab;
}

.calendar__days .cal-is-overdue {
  background-color: #ffccd2;
}
</style>
