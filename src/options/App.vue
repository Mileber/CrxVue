<template>
  <div id="app">
    <form id="options">
      <input type="checkbox" name="isActivated" checked />
      每
      <select name="frequency">
        <option v-for="item in minuteArr" :key="item">{{item}}</option>
      </select>
      分钟显示一个通知
      <button id></button>
    </form>
  </div>
</template>

<script>
export default {
  name: "app",
  data() {
    return {
      minuteArr: [1, 2, 3, 4, 5, 10, 15, 20, 25, 30],
      options: {}
    };
  },
  created: function() {
    console.log(localStorage);
    // Initialize the option controls.
    this.options.isActivated.checked = JSON.parse(localStorage.isActivated);
    // The display activation.
    this.options.frequency.value = localStorage.frequency;
    // The display frequency, in minutes.

    if (!this.options.isActivated.checked) {
      this.ghost(true);
    }

    // Set the display activation and frequency.
    this.options.isActivated.onchange = function() {
      localStorage.isActivated = this.options.isActivated.checked;
      this.ghost(!this.options.isActivated.checked);
    };

    this.options.frequency.onchange = function() {
      localStorage.frequency = this.options.frequency.value;
    };
  },
  methods: {
    ghost(isDeactivated) {
      this.options.style.color = isDeactivated ? "graytext" : "black";
      // The label color.
      this.options.frequency.disabled = isDeactivated; // The control manipulability.
    }
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-bottom: 60px;
}
</style>
