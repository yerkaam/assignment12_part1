<template>
  <div>
    <h1>Task Management</h1>

    <form @submit.prevent="addTask">
      <label for="taskTitle">Task Title:</label>
      <input v-model="newTask.title" type="text" id="taskTitle" required>

      <label for="completionStatus">Completion Status:</label>
      <input v-model="newTask.completed" type="checkbox" id="completionStatus">

      <button type="submit">Add Task</button>
    </form>

    <div>
      <h2>Incomplete Tasks</h2>
      <ul>
        <li v-for="task in incompleteTasks" :key="task.id">
          {{ task.title }} - Incomplete
          <button @click="toggleCompletion(task)">Mark Complete</button>
        </li>
      </ul>

      <h2>Completed Tasks</h2>
      <ul>
        <li v-for="task in completedTasks" :key="task.id">
          {{ task.title }} - Completed
          <button @click="toggleCompletion(task)">Mark Incomplete</button>
        </li>
      </ul>
    </div>

    <p>Total Incomplete Tasks: {{ incompleteTasks.length }}</p>
    <p>Total Completed Tasks: {{ completedTasks.length }}</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      tasks: [
        { id: 1, title: 'Task 1', completed: false },
        { id: 2, title: 'Task 2', completed: true },
      ],
      newTask: { title: '', completed: false },
    };
  },
  methods: {
    addTask() {
      if (this.newTask.title.trim() !== '') {
        this.tasks.push({ ...this.newTask, id: this.tasks.length + 1 });
        this.newTask.title = '';
        this.newTask.completed = false;
      }
    },
    toggleCompletion(task) {
      task.completed = !task.completed;
    },
  },
  computed: {
    incompleteTasks() {
      return this.tasks.filter((task) => !task.completed);
    },
    completedTasks() {
      return this.tasks.filter((task) => task.completed);
    },
  },
  watch: {
    tasks: {
      handler(newValue, oldValue) {
        console.log('Task list modified!');
      },
      deep: true,
    },
  },
  created() {
    console.log('Vue app created!');
  },
};
</script>

<style scoped>
</style>
