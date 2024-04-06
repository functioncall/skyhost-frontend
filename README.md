# Skyhost frontend

## Project setup
```
yarn install
```

### Make sure streaming source URL in valid OvenPlayer.vue
```
const player = OvenPlayer.create('player_id', {
    autoStart: true,
    controls: false,
    sources: [{
      label: 'label_for_webrtc',
      type: 'webrtc',
      file: 'ws://127.0.0.1:3333/app/stream'
    }]
  });
```

### Compiles and hot-reloads for development
```
yarn serve
```

### Compiles and minifies for production
```
yarn build
```

### Lints and fixes files
```
yarn lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).
