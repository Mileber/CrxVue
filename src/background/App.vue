<template>
  <div id="app">
    <!-- <img alt="Vue logo" src="../assets/icon.png"> -->
    <!-- <HelloWorld msg="Welcome to Your Background"/> -->
  </div>
</template>

<script>
export default {
  name: "app",
  created: function() {
    this.customTimer();
  },
  methods: {
    customTimer() {
      var that = this;
      // Conditionally initialize the options.
      if (!localStorage.isInitialized) {
        localStorage.isActivated = true; // The display activation.
        localStorage.frequency = 1; // The display frequency, in minutes.
        localStorage.isInitialized = true; // The option initialization.
      }

      // Test for notification support.
      if (window.Notification) {
        // While activated, show notifications at the display frequency.
        if (JSON.parse(localStorage.isActivated)) {
          that.show();
        }

        var interval = 0; // The display interval, in minutes.

        setInterval(function() {
          interval++;

          if (
            JSON.parse(localStorage.isActivated) &&
            localStorage.frequency <= interval
          ) {
            that.show();
            interval = 0;
          }
        }, 60000);
      }
    },
    show() {
      var time = /(..)(:..)/.exec(new Date()); // The prettyprinted time.
      var hour = time[1] % 12 || 12; // The prettyprinted hour.
      var period = time[1] < 12 ? "a.m." : "p.m."; // The period of the day.
      new Notification(hour + time[2] + " " + period, {
        icon: "../assets/icon.png",
        body: "在线打鸣"
      });
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
  margin-top: 60px;
}
</style>
