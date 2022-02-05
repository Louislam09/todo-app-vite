<template>
  <div class="container">
    <div class="calendar__container">
      <div class="calendar">
        <i
          @click="
            () => {
              this.showCalendar = !this.showCalendar;
            }
          "
          class="bx bxs-calendar"
          :class="isMobile && !showCalendar ? 'closed' : 'none'"
        ></i>
        <h3>February</h3>
        <div class="days">
          <div class="day">Sun</div>
          <div class="day">Mon</div>
          <div class="day">Tue</div>
          <div class="day">Wed</div>
          <div class="day">Thu</div>
          <div class="day">Fri</div>
          <div class="day">Sat</div>
          <div class="number"></div>
          <div class="number"></div>
          <calendar-day
            v-for="day in days"
            :key="day"
            :day="day"
            :show-modal="showModal"
          ></calendar-day>
        </div>
      </div>
      <div
        class="calendar_schedule"
        :class="isMobile && !showCalendar ? 'closed' : 'showCalendar'"
      >
        <i
          @click="
            () => {
              this.showCalendar = !this.showCalendar;
            }
          "
          class="bx bxs-calendar"
          :class="!isMobile ? 'closed' : 'none'"
        ></i>
        <h3>Schedule</h3>
        <div class="empty_event_state" v-if="!events.length">
          Not events to show
        </div>
        <div class="events_list">
          <ul>
            <event-item
              v-for="event in events"
              :key="event.id"
              :event="event"
              :removeEvent="removeEvent"
            />
          </ul>
        </div>
      </div>
    </div>
  </div>

  <teleport to="body">
    <Modal
      :show="openModal"
      :event="events[0]"
      :showModal="showModal"
      :addEvent="addEvent"
    />
  </teleport>
</template>

<script>
import EventItem from "./Schedule/EventItem.vue";
import Modal from "./Modal.vue";
import CalendarDay from "./CalendarDay.vue";
export default {
  name: "Calendar",
  components: {
    EventItem,
    Modal,
    CalendarDay,
  },
  data() {
    return {
      events: [],
      openModal: false,
      selectedEventDate: "",
      days: [
        1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20,
        21, 22, 23, 24, 25, 26, 27, 28,
      ],
      isMobile: false,
      showCalendar: false,
    };
  },
  methods: {
    addEvent(eventDescription) {
      const event = {
        id: this.events.length,
        number: this.events.length + 1,
        description: eventDescription,
        date: this.selectedEventDate,
      };

      this.events.push(event);
      this.showModal();
    },
    removeEvent(event) {
      console.log(event);
      this.events = this.events.filter((e) => e.id !== event.id);
    },
    showModal(day) {
      this.openModal = !this.openModal;
      this.selectedEventDate = day;
    },
    isMobileFunc() {
      this.isMobile = window.innerWidth < 768;
    },
  },
  mounted() {
    this.isMobileFunc();
    window.addEventListener("resize", this.isMobileFunc);
  },
  unmounted() {
    window.removeEventListener("resize", this.isMobileFunc);
  },
};
</script>

<style scoped>
.container {
  position: absolute;
  box-sizing: border-box;
  padding: 10px;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);
  width: 100%;
  max-width: 800px;
  height: 500px;
  border-radius: 5px;
  color: white;
  font-family: "Poppins", sans-serif;
}

.calendar__container {
  position: relative;
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 800px;
  height: 450px;
  background: var(--calendar-main-color);
  border: 15px solid var(--calendar-main-color);
  border-radius: 5px;
  box-shadow: 0 15px 35px rgba(0, 0, 0, 0.5);
  background: #fff;
}

.calendar {
  position: relative;
  width: 400px;
  padding: 30px;
  box-sizing: border-box;
}

.calendar_schedule i,
.calendar i {
  cursor: pointer;
  position: absolute;
  top: 10px;
  right: 10px;
  font-size: 50px;
  color: red;
  transition: all 0.3s ease-in-out;
}

.calendar_schedule i {
  color: white;
  top: 10px;
  right: 10px;
}

.calendar i.none {
  display: none;
}
.calendar_schedule i.closed {
  display: none;
}

.calendar .days {
  display: flex;
  flex-wrap: wrap;
}

.calendar h3 {
  padding: 0;
  margin: 0 0 20px;
  font-size: 24px;
  font-weight: bold;
  text-align: center;
  color: #1a314b;
}

.calendar .days .day,
.calendar .days .number {
  display: grid;
  place-items: center;
  width: 48px;
  height: 48px;
  color: #1a314b;
  cursor: pointer;
  transition: 0.1s ease;
}

.calendar .days .day:hover,
.calendar .days .number:hover {
  background: #1a314b79;
  color: #fff;
  /* border-radius: 50%; */
}

.calendar .days .day:first-child,
.calendar .days .number:nth-child(7n + 1) {
  color: red;
}

.calendar .days .number.active {
  background: #1a314b;
  color: #fff;
  border-radius: 50%;
}

.calendar__container .calendar_schedule {
  position: absolute;
  right: 0;
  top: 0;
  width: 400px;
  height: 100%;
  color: #1a314b;
  background: #1e436d;
  border-radius: 5px;
  box-shadow: 0 5px 10px rgba(0, 0, 0, 0.5);
  overflow: hidden;
  transition: all 0.3s ease-in-out;
}

.calendar__container .calendar_schedule h3 {
  position: relative;
  padding: 10px 0 0;
  font-size: 24px;
  font-weight: bold;
  text-align: center;
  color: white;
  font-weight: bold;
}
.calendar__container .calendar_schedule h3::after {
  position: absolute;
  content: "";
  display: block;
  width: 24%;
  height: 2px;
  bottom: 0;
  left: 36%;
  text-align: center;
  background: white;
}

.calendar_schedule .events_list {
  padding: 20px;
  height: 100%;
  overflow-y: auto;
  overflow: auto;
  padding-bottom: 50px;
}

.calendar_schedule .events_list ul {
  list-style: none;
  padding: 0;
  margin: 0;
}

.empty_event_state {
  position: absolute;
  top: 30%;
  left: 50%;
  transform: translate(-50%, -50%);
  font-size: 20px;
  font-weight: bold;
  text-align: center;
  padding: 20px 10px;
  width: 80%;
  border: 0.1px solid #ffffff28;
  color: white;
  border-radius: 5px;
  box-shadow: 0 5px 10px rgba(0, 0, 0, 0.5);
  background: linear-gradient(
    to left,
    rgba(0, 0, 0, 0.5) 0%,
    rgba(0, 0, 0, 0.5) 50%,
    rgba(0, 0, 0, 0) 100%
  );
  margin: 0 0 15px;
}

.calendar_schedule.closed {
  z-index: -1;
}
.calendar_schedule.showCalendar {
  z-index: 999;
}

ul::-webkit-scrollbar {
  width: 10px;
}

ul::-webkit-scrollbar-track {
  box-shadow: inset 0 0 6px rgba(0, 0, 0, 0.8);
  border-radius: 15px;
}

ul::-webkit-scrollbar-thumb {
  border-radius: 15px;
  background-color: var(--calendar-main-color);
}

@media (max-width: 768px) {
  .calendar__container {
    width: 100%;
    height: 100%;
    border: none;
    box-shadow: none;
    flex-direction: column;
  }

  .calendar {
    z-index: 2;
  }
}
</style>