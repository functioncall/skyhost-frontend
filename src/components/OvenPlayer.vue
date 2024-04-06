<template>
  <div id="player_id" style="width: 100%; height: 500px;"></div>
</template>

<script>
/* global OvenPlayer */
export default {
  name: 'OvenPlayerComponent',
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
        sources: [{
          label: 'label_for_webrtc',
          type: 'webrtc',
          file: 'ws://127.0.0.1:3333/app/stream'
        }]
      });

      player.on('ready', () => {
      if (player.getConfig() && player.getConfig().systemText && player.getConfig().systemText.api && player.getConfig().systemText.api.error) {
        player.getConfig().systemText.api.error[501] = { message: 'Waiting for live streaming.' };
      }
    });
    }
  }
}
</script>
