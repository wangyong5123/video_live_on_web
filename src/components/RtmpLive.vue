<template>
  <video-player class="vjs-custom-skin"
    ref="videoPlayer"
    :options="playerOptions"
    :playsinline="true"
    customEventName="customstatechangedeventname">
  </video-player>
</template>

<script>
import 'videojs-flash'
export default {
  name: 'rtmp-live',
  props: {
    src: {
      type: String,
      default: 'rtmp://192.168.1.106:2018/live'
    }
  },
  data () {
    return {
      playerOptions: {
        // height: '320',
        // width: '100%',
        sources: [ {
          type: 'rtmp/h264',
          src: this.src
        } ],
        techOrder: ['flash'],
        autoplay: true, // 自动播放
        controls: true, // 控制条
        fluid: true, // 按比例缩放适应容器
        preload: 'auto', // 预加载
        // muted: true, // 消除所有音频
        loop: false, // 循环播放
        aspectRatio: "16:9",
      }
    }
  }
}
</script>