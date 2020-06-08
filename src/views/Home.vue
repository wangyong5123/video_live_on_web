<template>
  <div class="home">
    <div class="title">{{ title }}</div>
    <div class="subtitle">{{ subtitle }}</div>
    <Row type="flex" justify="center" :gutter="20">
      <Col :span="18">
        <Row type="flex" justify="start" :gutter="20" >
          <i-col :span="12" v-for="(item, i) in videoInfo" :key="`info-${i}`" style="margin-bottom:30px;">
            <Card>
              <p slot="title" style="">{{ item.title }}</p>
              <div >
                <RtmpLive :src="item.videoSrc"></RtmpLive>
              </div>
            </Card>
          </i-col>
        </Row>
      </Col>
    </Row>
  </div>
</template>

<script>
import GithubButton from 'vue-github-button'
import RtmpLive from "@/components/RtmpLive.vue";


export default {
  name: "home",
  components: {
    GithubButton,
    RtmpLive,
  },
  data () {
    return {
      title: ' 播放视频流/直播',
      subtitle: ' ',
      videoInfo: [
        { title: '视频1', videoSrc: 'rtmp://192.168.1.100:2018/live/'},
        { title: '视频2', videoSrc: 'rtmp://192.168.1.100:2018/live/'},

      ],
      imgSrc: '', // 图片路径
      canvas: '',
      context: '',
      videoTag: ''
    }
  },
  mounted () {
    this.videoTag = document.getElementById('videoElement2')
    this.canvas = document.getElementById('canvas')
    this.context = this.canvas.getContext('2d')
    console.log('加载数据：', this.videoTag, this.canvas, this.context)
  },
  methods: {
    captureImg () {
      this.context.drawImage(this.videoTag, 0, 0, 515, 300)
      let base64 = this.canvas.toDataURL('image/jpeg')
      console.log('base64:', base64)
      this.imgSrc = base64
    }
  }
};
</script>

<style lang="less" scoped>
a {
  // color: #42b983;
  color: #fff;
}
a:hover {
  color: #fff;
}
.title {
  height: 1em;
  line-height: 1em;
  font-weight: 700;
  font-size: 4rem;
  margin: 1.5em 0 1.2em;
}
.subtitle {
  font-size: 1.8em;
  color: #a5a5a5;
  margin: 1em 0;
  font-weight: bold;
}
.actions {
  margin-top: 3em;
  margin-bottom: 2em;
}
.example-title {
  font-size: 1.8em;
  font-weight: bold;
  margin-top: 3em;
  margin-bottom: 2em;
}
</style>

