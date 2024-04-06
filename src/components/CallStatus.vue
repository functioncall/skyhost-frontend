<template>
  <div class="call-status">
    <span class="status-indicator">
      <img class="logo" src="@/assets/logo.png" alt="Logo">
    </span>
    <span class="message">Flight is<br>in progress</span>
    <span class="timer-container">
      <span class="timer">{{ formattedDuration }}</span>
    </span>
  </div>
</template>

<script>
export default {
  name: 'CallStatus',
  data() {
    return {
      startTime: Date.now(),
      duration: 0
    };
  },
  computed: {
    formattedDuration() {
      const seconds = Math.floor(this.duration % 60);
      const minutes = Math.floor((this.duration / 60) % 60);
      return `${minutes.toString().padStart(2, '0')}:${seconds.toString().padStart(2, '0')}`;
    }
  },
  created() {
    this.updateTimer();
  },
  methods: {
    updateTimer() {
      setInterval(() => {
        this.duration = Math.floor((Date.now() - this.startTime) / 1000);
      }, 1000);
    }
  }
}
</script>

<style scoped>
.call-status {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px 10px;
  background-color: #f0f0f0;
  border-radius: 40px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  font-size: 0.9em;
  color: #333;
}

.status-indicator {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 50px;
  width: 50px;
  background-color: #E2E5ED;
  border-radius: 50%;
  margin-right: 10px;
  overflow: hidden;
}

.logo {
  width: 20px; /* Adjust width as necessary */
  height: 20px; /* Adjust height to maintain aspect ratio */
}

.message {
  flex-grow: 1;
  text-align: left;
  margin-right: 10px;
  font-weight: 600;
  color: black;
}

.timer-container {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 50px;
  width: 80px;
  background-color: #E2E5ED;
  border-radius: 25px;
  margin-right: 10px;
  overflow: hidden;
  margin: 0 auto;
}

.timer {
  min-width: 50px;
}
</style>