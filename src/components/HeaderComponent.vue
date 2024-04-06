<template>
  <div class="header">
    <span class="title">Skyhost</span>
    <span class="time">{{ currentTime }}</span>
  </div>
</template>

<script>
export default {
  name: 'HeaderComponent',
  data() {
    return {
      currentTime: this.getCurrentTime()
    };
  },
  created() {
    setInterval(() => {
      this.currentTime = this.getCurrentTime();
    }, 1000 * 60); // Update the time every minute
  },
  methods: {
    getCurrentTime() {
      const now = new Date();
      return now.toLocaleTimeString('en-US', { hour: '2-digit', minute: '2-digit', hour12: true });
    }
  }
}
</script>

<style scoped>
.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 100%;
  padding: 10px;
  box-sizing: border-box;
  color: #fff;
}

.title {
  margin-left: 20px;
}

.time {
  margin-right: 20px;
}
</style>