<template>
  <section class="new-task">
    <input type="text" placeholder="New task" v-model="newTaskInfo.newTask" />
    <input type="date" v-model="newTaskInfo.newTaskDate" />
    <input type="submit" @click="sendTaskToParent()" value="Add New Task" />
  </section>
</template>

<script>
export default {
  name: "NewTask",
  props: {},
  data: function() {
    return {
      newTaskInfo: {
        newTask: "",
        newTaskDate: "",
      },
    };
  },
  methods: {
    sendTaskToParent() {
      this.$emit("add-task-to-list", this.newTaskInfo);
    },
  },
};
</script>

<style scoped>
.new-task {
  display: flex;
  justify-content: space-between;
  margin-bottom: 75px;
}

.new-task input {
  padding: 10px;
  font-size: 20px;
  color: #444;
  border: 2px solid #ddd;
  border-radius: 2px;
  font-family: inherit;
  flex-basis: 35%;
}

.new-task input[type="submit"] {
  background-color: OliveDrab;
  color: white;
  cursor: pointer;
  font-family: "Assistant", sans-serif;
  flex-basis: 22%;
  transition: all 0.3s;
}

.new-task input[type="submit"]:hover {
  background: white;
  color: OliveDrab;
  font-weight: bold;
  border-color: OliveDrab;
  border-width: 2px;
}

.new-task input[type="submit"]:focus {
  outline: 1px solid white;
}

input::placeholder {
  color: #aaa;
}


</style>
