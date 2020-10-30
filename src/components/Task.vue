<template>
  <span class="task">
    <input
      type="checkbox"
      @input="$emit('change-done-status')"
      v-bind:checked="task.isDone"
    />
    <div
      :class="[
        { overdue: task.isOverdue && !task.isDone, done: task.isDone },
        'task__content',
      ]"
    >
      <p class="task__name">{{ task.taskName }}</p>
      <p class="task__date">{{ formatDate(task.dueDate) }}</p>
    </div>
  </span>
</template>

<script>
export default {
  name: "Task",
  props: { task: Object, months: Array },
  methods: {
    formatDate(date) {
      let day = date.split("-")[2];
      let monthNum = date.split("-")[1];
      let month = this.months[monthNum - 1].slice(0, 3);
      return `${day} ${month}`;
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.task {
  width: 100%;
  height: 60px;
  position: relative;
  display: flex;
  align-items: center;
  border: 1px solid #ddd;
  margin-bottom: 25px;
  background-color: #f7f7f7;
  box-shadow: 0px 1px 10px #ddd;
  color: #444;
}

.task input[type="checkbox"] {
  margin: 0 20px 0 10px;
}

.task__content {
  display: flex;
  align-items: center;
  justify-content: space-between;
  width: 80%;
}

.task__name {
  margin: 0;
  font-size: 21px;
  border: none;
  background-color: transparent;
}

.task__date {
  margin: 0;
  font-size: 19px;
}

.overdue {
  color: red;
}

.done {
  text-decoration: line-through;
  color: #888;
}
</style>
