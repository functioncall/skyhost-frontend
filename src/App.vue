<template>
  <div id="app">
    <div class="player-wrapper">
      <div class="header">
        <div class="title-container">
          <h1 class="app-title">Skyhost</h1>
          <p class="flight-portal">
            Flight Portal
          </p>
        </div>
        <CallStatus class="app-title" />
      </div>
      <OvenPlayer />
    </div>
    <div class="footer">
      <h3 class="current-time">{{ currentTime }} | <span class="location">Mt. Takao Hachioji, Japan</span></h3>
      <button class="microphone-button" @click="toggleMicrophone">
        <i :class="microphoneIcon"></i>
      </button>
    </div>
  </div>
</template>

<script>
import OvenPlayer from './components/OvenPlayer.vue'
import CallStatus from './components/CallStatus.vue'

export default {
  name: 'App',
  components: {
    OvenPlayer,
    CallStatus,
  },
  data() {
    return {
      currentTime: this.getCurrentTime(),
      isMicrophoneOn: false
    };
  },
  computed: {
    microphoneIcon() {
      return this.isMicrophoneOn ? 'fas fa-microphone' : 'fas fa-microphone-slash';
    }
  },
  created() {
    setInterval(() => {
      this.currentTime = this.getCurrentTime();
    }, 1000 * 60); // Update the time every minute
  },
  methods: {
    getCurrentTime() {
      const now = new Date();
      const jstTime = new Date(now.toLocaleString('en-US', { timeZone: 'Asia/Tokyo' }));
      const timeString = jstTime.toLocaleTimeString('en-US', { hour: '2-digit', minute: '2-digit', hour12: true }).replace('PM', 'pm').replace('AM', 'am');
      return `${timeString} JST`;
    },
    toggleMicrophone() {
      console.log('Toggle microphone button clicked');
      this.isMicrophoneOn = !this.isMicrophoneOn;
    }
  }
}
</script>

<style>
html, body {
  height: 100%; /* Set the height to match the viewport */
  margin: 0; /* Remove default margin */
  overflow: hidden; /* Disable scrolling */
  background-color: black; /* Set the background color to black */
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
}

.title-container {
  margin-left: 50px;
  justify-content: center;
}

.header {
  position: absolute;
  top: 0;
  display: flex;
  z-index: 10;
  justify-content: space-between;
  align-items: center;
  width: 100%;
  overflow: hidden;
}

.app-title {
  font-size: 42px;
  color: #fff;
  margin-bottom: -20px; /* Reduce the gap */
}

.flight-portal {
  font-size: 18px;
  font-weight: 100;
  color: #f0f0f0;
  text-align: left;
}

.footer {
  position: absolute;
  bottom: 0;
  width: 100%;
  z-index: 10;
  display: flex;
  justify-content: space-between;
  align-items: center;
  color: #fff;
  padding: 10px;
}

.player-wrapper {
  position: relative;
  width: 100%; /* Adjust based on your needs */
  /* height: 500px; Adjust based on your needs */
}

.call-status {
  color: #fff;
  margin-right: 50px;
}

.timer-container {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 50px;
  width: 70px;
  background-color: #E8EBF2;
  border-radius: 25px;
  margin-right: 10px;
  overflow: hidden;
  margin: 0 auto; /* Center the timer horizontally */
}

.message {
  color: #fff;
  margin-right: 50px;
}

.location {
  font-size: 15px;
  font-weight: bold;
  color: #f0f0f0;
  display: inline-block;
  width: 150px;
  word-wrap: break-word;
  text-align: left;
  opacity: 0.5;
}

.current-time {
  font-size: 44px;
  color: #fff;
  margin-left: 50px;
  font-weight: 100;
  font-family: 'Public Sans', sans-serif;
  justify-content: center;
  align-items: center;
}

.microphone-button {
  width: 70px;
  height: 70px;
  margin-right: 50px;
  border-radius: 50%;
  background-color: #F97474;
  color: #fff;
  display: flex;
  justify-content: center;
  align-items: center;
  margin-top: 20px;
  border-width: 0;
}

.microphone-button i {
  font-size: 24px; /* Set the font size of the icon to 18px */
}

</style>
