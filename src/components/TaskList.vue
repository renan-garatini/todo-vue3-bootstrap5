<template>
  <div class="taskList row">
    <template v-if="tasks.length">
      <Task
        v-for="(task) in tasks"
        :key="task.name"
        :task="task"
        @deleteTask="this.$emit('deleteTask', $event)"
        @changeStateTask="this.$emit('changeStateTask', $event)"
      ></Task>
    </template>
    <p v-else class="no-task">Sem tarefas :)</p>
  </div>
</template>

<script>
import Task from "@/components/Task.vue";

export default {
  components: {
    Task,
  },
  props: {
    tasks: {
      type: Array,
      required: true,
    },
  },
};
</script>

<style>
</style>