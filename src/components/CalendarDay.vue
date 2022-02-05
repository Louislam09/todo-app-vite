<template>
  <div
    @click="showModal(day)"
    class="number"
    :class="day === currentDay && 'active'"
  >
    {{ day }}
  </div>
</template>

<script>
export default {
  name: "CalendarDay",
  props: {
    day: Number,
    showModal: Function,
  },
  data() {
    return {
      currentDay: new Date().getDate(),
    };
  },
};
</script>

<style scoped>
</style>