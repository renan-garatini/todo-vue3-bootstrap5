<template>
  <div class="container">
    <h1 class="display-5">Tarefas</h1>
    <NewTask @addTask="saveTask"></NewTask>
    <hr />
    <TaskProgress :progress="progress"></TaskProgress>
    <hr />
    <TaskList
      :tasks="tasks"
      @deleteTask="removeTask"
      @changeStateTask="toggleTaskPending"
    />
  </div>
</template>

<script>
import TaskList from "@/components/TaskList.vue";
import NewTask from "@/components/NewTask.vue";
import TaskProgress from "@/components/TaskProgress.vue";
export default {
  components: { TaskList, NewTask, TaskProgress },
  data() {
    return {
      tasks: [],
    };
  },
  watch: {
    tasks: {
      deep: true,
      handler() {
        localStorage.setItem("tasks", JSON.stringify(this.tasks));
      },
    },
  },
  created() {
    const json = localStorage.getItem("tasks");
    this.tasks = JSON.parse(json) || [];
  },
  computed: {
    progress() {
      const totalTasks = this.tasks.length;

      if (totalTasks == 0) return 100;

      const verifyDoneTasks = (t) => t.pending === false;
      const taskDone = this.tasks.filter(verifyDoneTasks).length;

      return Math.round((taskDone / totalTasks) * 100);
    },
  },
  methods: {
    saveTask(task) {
      const verifyNameAlreadyExist = (t) => t.name === task.name;
      const isNewName = this.tasks.filter(verifyNameAlreadyExist).length === 0;
      if (isNewName) this.tasks.push({ name: task.name, pending: true });
    },
    removeTask(deleteTask) {
      const removeTaskIndex = this.tasks.findIndex((task) => {
        if (deleteTask.name == task.name) return true;
      });

      this.tasks.splice(removeTaskIndex, 1);
    },
    toggleTaskPending(taskChanged) {
      const changedTaskIndex = this.tasks.findIndex((task) => {
        if (taskChanged.name == task.name) return true;
      });

      this.tasks[changedTaskIndex].pending = !this.tasks[changedTaskIndex]
        .pending;
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
