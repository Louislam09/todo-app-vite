<template>
  <div class="container">
    <h2>{{ title }}</h2>
    <h6>(code + phone number)</h6>
    <div class="input__box">
      <input v-model="phoneNumber" type="text" required />
      <label>Phone Number</label>
    </div>
    <p v-if="errorMessage" class="error">{{ errorMessage }}</p>

    <button @click="add">Add</button>

    <!-- <p v-if="tasks.length === 0" class="empty__state">No tasks yet</p> -->
  </div>
</template>

<script>
export default {
  name: "WaMe",
  props: {
    title: String,
  },
  data() {
    return {
      phoneNumber: "",
      errorMessage: "",
    };
  },
  methods: {
    add: function () {
      if (!this.phoneNumber) {
        this.errorMessage = "Phone number cannot be empty";
        return;
      }
      const baseUrl = `https://wa.me/${this.phoneNumber}?text=`;
      window.open(baseUrl, "_blank");
      this.phoneNumber = "";
    },
  },
};
</script>

<style scoped>
p.error {
  text-align: center;
  text-transform: uppercase;
  margin: 2px 0px 14px 0px;
  color: color;
  background: rgba(255, 0, 0, 0.5);
  padding: 5px;
}

.container {
  width: 400px;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);
  position: absolute;
  padding: 40px;
  box-sizing: border-box;
  border-radius: 10px;
  background: rgba(0, 0, 0, 0.6);
  background: rgba(18, 140, 126, 0.6);
  color: white;
  box-shadow: 0 15px 25px rgba(0, 0, 0, 0.5);
  text-align: left;
  font-weight: bold;
  font-family: Poppins, sans-serif;
}

.container h2,
h6 {
  text-align: center;
}

.input__box {
  position: relative;
}

.input__box input {
  width: 100%;
  border: none;
  outline: none;
  background: transparent;
  color: white;
  font-size: 16px;
  padding: 10px 0;
  margin-bottom: 30px;
  border-bottom: 1px solid #fff;
}

.input__box label {
  position: absolute;
  top: 0;
  left: 0;
  padding: 10px 0;
  font-size: 16px;
  color: #fff;
  pointer-events: none;
  transition: 0.2s ease all;
}

.input__box input:focus ~ label,
.input__box input:valid ~ label {
  top: -18px;
  left: 0;
  color: #01e675;
  font-size: 12px;
  pointer-events: none;
}

.container button {
  background: transparent;
  border: none;
  outline: none;
  color: white;
  background: #01e675;
  padding: 10px 20px;
  width: 100%;
  border-radius: 5px;
  cursor: pointer;
  transition: 0.2s ease all;
  left: 0%;
  text-transform: uppercase;
  font-weight: bold;
}

.empty__state {
  text-align: center;
  color: #fff;
  font-size: 16px;
  margin-top: 20px;
  padding: 10px;
  background: rgba(106, 119, 122, 0.432);
  box-shadow: 0 15px 25px rgba(0, 0, 0, 0.5);
}
</style>
