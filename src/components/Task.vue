<template>
  <div class="col-md-3 p-1">
    <div class="card task text-center text-white" :class="stateClass" @click="changeStateTask">
      <div class="card-content m-auto">
        <div class="close" @click.stop="deleteTask">x</div>
        <div class="card-text">
          <p>{{ task.name }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    task: {
      type: Object,
      required: true,
    },
  },
  methods: {
    deleteTask() {
      this.$emit('deleteTask',this.task);
    },
    changeStateTask(){
      this.$emit('changeStateTask',this.task);
    }
  },
  computed: {
    stateClass() {
      return {
        "bg-danger": this.task.pending,
        "bg-success": !this.task.pending,
      };
    },
  },
};
</script>

<style scoped>
.task {
  height: 100px;
  user-select: none;
}

.bg-success {
  text-decoration: line-through;
}

.close {
  display: flex;
  position: absolute;
  top: 5px;
  right: 10px;
}
</style>