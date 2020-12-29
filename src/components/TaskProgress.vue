<template>
  <div class="taskProgress">
    <span class="progressValue">{{ progress }}%</span>
    <div class="progress">
      <div
        class="progress-bar"
        role="progressbar"
        :style="{ width: progress + '%' }"
        :aria-valuenow="progress"
        aria-valuemin="0"
        aria-valuemax="100"
      ></div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    progress: {
      type: Number,
      required: true,
    },
  },
};
</script>

<style>
</style>