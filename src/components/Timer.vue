<template>
  <div class="container">
    <div class="content">
      <div class="time_remaining_section">
        <div class="title">Digital Clock</div>
        <div class="time">
          <div class="hour">
            <span>{{ time.hours }}&nbsp;:&nbsp;</span>
            <span>hours</span>
          </div>
          <div class="mins">
            <span>{{ time.mins }}&nbsp;:&nbsp;</span>
            <span>minutes</span>
          </div>
          <div class="secs">
            <span>{{ time.secs }}</span>
            <span>seconds</span>
          </div>
        </div>
      </div>

      <div class="deadline_section">
        <div class="line"></div>
        <div class="title">Calendar</div>
        <div class="dayMonth">
          <span>{{ time.day }}</span>
          <span>{{ time.shortMonth }}</span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Timer",
  components: {},
  data: () => ({
    time: {
      hours: "00",
      mins: "00",
      secs: "00",
      day: "00",
      shortMonth: "Jan",
    },
  }),
  mounted() {
    const appendZero = (number) =>
      number < 10 ? (number = `0${number}`) : number;
    const getHour = () => {
      let date = new Date();
      let hours = date.getHours();
      let minutes = date.getMinutes();
      let seconds = date.getSeconds();
      let currentDay = date.getDate();
      let currentShortMonth = date.toDateString().split(" ")[1];

      // let format = hours >= 12 ? 'P.M' : 'A.M';
      hours = hours % 12 || 12;

      this.time.hours = hours;
      this.time.mins = appendZero(minutes);
      this.time.secs = appendZero(seconds);
      this.time.secs = appendZero(seconds);
      this.time.day = appendZero(currentDay);
      this.time.shortMonth = appendZero(currentShortMonth);
    };

    const interval = setInterval(() => {
      getHour();
    }, 1000);
  },
};
</script>

<style>
body {
  color: white;
  background: url(assets/bg.jpg);
  background-size: cover;
}
</style>

<style scoped>
.container {
  box-sizing: border-box;
  padding: 10px;
  position: absolute;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);
  width: 600px;
  height: 200px;
  border-radius: 5px;
  color: white;
  background: rgba(15, 21, 31, 0.8);
  box-shadow: 0 15px 25px rgba(250, 112, 102, 0.5);
}

.content {
  position: relative;
  box-sizing: border-box;
  width: 100%;
  height: 100%;
  display: flex;
}

.content .time_remaining_section,
.deadline_section {
  display: flex;
  flex-direction: column;
  flex: 0.8;
  padding: 10px 30px;
  align-items: center;
  font-family: "Poppins", sans-serif;
}
.content .time_remaining_section .title,
.deadline_section .title {
  text-align: start;
  width: 100%;
  color: white;
  margin-bottom: 5px;
  font-family: "Poppins", sans-serif;
  font-weight: 600;
  font-size: 20px;
}

.content .time_remaining_section .time,
.dayMonth {
  display: flex;
  align-items: center;
  justify-content: space-between;
  width: 100%;
  font-weight: 300;
}

.time > div,
.dayMonth {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.time > div > span:first-child,
.dayMonth > span:first-child {
  color: #fff20e;
  font-size: 3.5rem;
}

.time > div > span:last-child,
.dayMonth > span:last-child {
  font-weight: 100;
  text-transform: uppercase;
  width: 100%;
  text-align: start;
  padding-left: 4px;
}
.dayMonth > span:last-child {
  text-align: center;
}
.deadline_section {
  position: relative;
  display: flex;
  flex-direction: column;
  flex: 0.4;
}

.deadline_section .line {
  position: absolute;
  left: 0;
  top: 20px;
  height: 75%;
  width: 2px;
  background: white;
}

.deadline_section .title {
  text-align: center;
}
</style>