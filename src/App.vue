<template>
  <div class="container">
    <h1>To-do list</h1>
    <section class="tasks">
      <p v-if="todoList.length == 0">You currently have no tasks.</p>
      <ul v-else>
        <li v-for="task in todoList" :key="task.taskName">
          <Task
            :task="task"
            :months="months"
            @change-done-status="task.isDone = !task.isDone"
          />
        </li>
      </ul>
    </section>
    <NewTask @addTaskToList="addTaskToList($event)" />
    <Calendar :todoList="todoList" />
  </div>
</template>

<script>
import Task from "./components/Task.vue";
import NewTask from "./components/NewTask.vue";
import Calendar from "./components/Calendar.vue";

export default {
  name: "App",
  components: {
    Task,
    NewTask,
    Calendar,
  },
  data: function() {
    return {
      todoList: [
        {
          taskName: "Do laundry",
          dueDate: "2021-02-01",
          isDone: false,
          isOverdue: false,
        },
        {
          taskName: "Register for the course",
          dueDate: "2021-02-04",
          isDone: false,
          isOverdue: false,
        },
        {
          taskName: "Complete the course",
          dueDate: "2021-02-17",
          isDone: false,
          isOverdue: false,
        },
      ],
      months: [
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
      ],
    };
  },
  methods: {
    addTaskToList(event) {
      let newTask = {};
      console.log(event);
      newTask.taskName = event.newTask;
      newTask.dueDate = event.newTaskDate;
      newTask.isDone = false;
      newTask.isOverdue =
        new Date(this.newTaskDate) < new Date() ? true : false;
      this.todoList.push(newTask);
      this.sortByDate();
      this.newTask = "";
      this.newTaskDate = "";
    },
    sortByDate() {
      this.todoList.sort((a, b) => new Date(a.dueDate) - new Date(b.dueDate));
    },
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Ubuntu:wght@300;700&display=swap");
* {
  box-sizing: border-box;
}

:root {
  color: #444;
}

.container {
  font-family: "Ubuntu", sans-serif;
  width: 800px;
  margin: 0 auto;
}

h1,
h2 {
  color: olivedrab;
  text-align: center;
}

h1 {
  margin: 60px 0 40px 0;
}

ul {
  padding-left: 0;
  margin-bottom: 40px;
  list-style: none;
}
</style>
