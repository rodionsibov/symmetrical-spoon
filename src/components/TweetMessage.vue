<template>
  <p class="rounded p-2 m-0" style="background: #f0f0f0">
    {{ tweet.text }}
  </p>
  <div class="form-text d-flex align-items-center justify-content-between">
    <div class="d-flex align-items-center gap-1">
      <i class="fas fa-calendar-alt fa-sm fa-fw"></i>
      <span>
        {{ tweet.date }}
      </span>
    </div>
    <button
      @click="$emit('remove-tweet', index)"
      title="Delete this tweet"
      class="text-danger btn p-0"
    >
      <i class="fas fa-trash fa-sm fa-fw"></i>
    </button>
  </div>
</template>

<script>
export default {
  props: ["tweet"],
  emits: ["remove-tweet"],
};
</script>

<style>
</style>