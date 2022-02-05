<template>
  <div class="modal" v-if="show">
    <div class="modal__content">
      <div class="close" @click="showModal">&times;</div>
      <h3>Add event</h3>
      <div class="form">
        <div class="input__box">
          <textarea required type="text" rows="4" v-model="eventDescription" />
          <label>Event description</label>
        </div>

        <div class="form__group">
          <button
            class="btn"
            @click="
              () => {
                addEvent(eventDescription);
                eventDescription = '';
              }
            "
          >
            Add event
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Modal",
  props: {
    show: Boolean,
    event: Object,
    showModal: Function,
    addEvent: Function,
  },
  data() {
    return {
      eventDescription: "",
    };
  },
};
</script>

<style scoped>
.modal__content {
  padding: 20px;
  background-color: rgb(26, 49, 75);
  background: linear-gradient(
    to left,
    rgb(26, 49, 75) 0%,
    rgba(26, 134, 148, 0.5) 50%,
    rgba(26, 49, 75) 100%
  );
  box-shadow: 0 0 20px rgba(0, 0, 0, 0.5);
  border-radius: 5px;
  width: 40%;
  margin: 0 auto;
  position: relative;
  color: white;
  display: flex;
  flex-direction: column;
  justify-content: center;
}

.modal__content .close {
  position: absolute;
  right: 6px;
  top: -5px;
  color: var(--calendar-main-color);
  cursor: pointer;
  font-size: 2rem;
}
.modal__content .close:hover {
  color: var(--calendar-main-color-hover);
  transform: rotate(360deg);
  transition: transform 0.4s ease;
}

.modal__content h3 {
  background: linear-gradient(
    to left,
    rgba(0, 0, 0, 0.5) 0%,
    rgba(0, 0, 0, 0.5) 50%,
    rgba(0, 0, 0, 0.5) 100%
  );
  padding: 10px;
  text-align: center;
  margin: 0 0 20px;
  text-transform: uppercase;
}

.modal__content .input__box {
  position: relative;
}

.modal__content .input__box textarea {
  width: 100%;
  border: none;
  outline: none;
  background: transparent;
  color: white;
  font-size: 16px;
  padding: 10px 0;
  margin-bottom: 30px;
  border: 1px solid #fff;
  border-radius: 5px;
  padding: 10px;
}

.modal__content .input__box label {
  position: absolute;
  top: 0;
  left: 10px;
  padding: 10px 0;
  font-size: 16px;
  color: #fff;
  pointer-events: none;
  transition: 0.2s ease all;
}

.modal__content .input__box textarea:focus ~ label,
.modal__content .input__box textarea:valid ~ label {
  top: -10px;
  left: 8px;
  color: var(--calendar-main-color);
  font-size: 12px;
  pointer-events: none;
  background: linear-gradient(
    to left,
    rgb(26 49 75 / 0%) 0%,
    rgb(0 79 89) 50%,
    rgb(26 49 75 / 0%) 100%
  );
  padding: 2px 2px;
}

button {
  background: transparent;
  border: none;
  outline: none;
  color: #000;
  background: var(--calendar-main-color);
  padding: 10px 20px;
  width: 100%;
  border-radius: 5px;
  cursor: pointer;
  transition: 0.2s ease all;
  left: 0%;
}

@media (max-width: 768px) {
  .modal__content {
    width: 90%;
  }
}
</style>