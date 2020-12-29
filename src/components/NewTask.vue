<template>
  <div class="newTask row">
    <div class="col-md-11">
      <input type="text" v-model="name" @keydown.enter="add" class="form-control" />
    </div>
    <div class="col-md-1">
      <button class="btn btn-success" @click="add">+</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      name: "",
    };
  },
  methods: {
    add() {
      this.$emit("addTask", { name: this.name });
      this.name = '';
    },
  },
};
</script>

<style>
</style>