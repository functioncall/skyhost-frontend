<template>
  <div id="player_id" style="width: 100%; height: 500px;"></div>
</template>

<script>
/* global OvenPlayer */
export default {
  name: 'OvenPlayerComponent',
  data() {
    return {
      isReloading: false,
      isStreaming: false,
    };
  },
  mounted() {
    this.loadOvenPlayerScript().then(() => {
      this.setupPlayer();
    });
  },
  methods: {
    loadOvenPlayerScript() {
      return new Promise((resolve, reject) => {
        const script = document.createElement('script');
        script.src = "https://cdn.jsdelivr.net/npm/ovenplayer/dist/ovenplayer.js";
        script.onload = resolve;
        script.onerror = reject;
        document.head.appendChild(script);
      });
    },
    setupPlayer() {
      const player = OvenPlayer.create('player_id', {
        autoStart: true,
        controls: false,
        autoFallback: true,
        mute: true,
        sources: [{
          label: 'jp_webrtc',
          type: 'webrtc',
          file: 'ws://127.0.0.1:3333/app/stream'
        }]
      });

      player.on('player_state', () => {
        console.log('Stream is ready');
        player.play(); 
      });

      player.on('play', () => {
        this.isStreaming = true; // Set isStreaming to true when stream starts playing
        console.log('Stream started playing', this.isStreaming);
      });

      player.on('error', () => {
        this.isStreaming = false; // Set isStreaming to false when stream stops
        console.log('Stream stopped', this.isReloading);
        if (!this.isReloading) {
          this.isReloading = true;
          setTimeout(() => {
            this.loadOvenPlayerScript().then(() => {
              this.setupPlayer();
              this.isReloading = false; // Reset the flag after reload
            });
          }, 1000);
        }
  });
    }
  }
}
</script>

