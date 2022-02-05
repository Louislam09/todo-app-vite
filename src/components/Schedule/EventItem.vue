<template>
  <li>
    <div class="event">
      <div class="event__content">
        <span class="close" @click="removeEvent(event)">&times;</span>
        <h4>Event {{ event.number }}</h4>
        <p>{{ event.description }}</p>
      </div>
      <div class="event__date">
        <span>{{ date }}</span>
      </div>
    </div>
  </li>
</template>

<script>
export default {
  name: "EventItem",
  props: ["event", "removeEvent"],
  components: {},
  computed: {
    date: function () {
      const d = new Date();
      return new Date(
        `${d.getMonth() + 1}/${this.event.date}/${d.getFullYear()}"`
      ).toDateString();
    },
  },
};
</script>

<style scoped>
.calendar_schedule .events_list ul li {
  padding: 10px 0;
  border: 0.1px solid rgba(255, 255, 255, 0.158);
  color: white;
  border-radius: 5px;
  padding: 5px 10px;
  box-shadow: 0 5px 10px rgba(0, 0, 0, 0.5);
  background-color: #1a314b;
  background: linear-gradient(
    to left,
    rgba(0, 0, 0, 0.5) 0%,
    rgba(0, 0, 0, 0.5) 50%,
    rgba(0, 0, 0, 0) 100%
  );
  margin: 0 0 15px;
}
.event__content {
  position: relative;
}
.event__content p {
  font-style: italic;
  font-size: 14px;
  color: white;
}

.event__content .close {
  position: absolute;
  right: 0;
  top: 0;
  cursor: pointer;
}

.event__date {
  text-align: end;
  font-size: 12px;
}
</style>