<template>
  <div>
    <div class="video-x">
      <canvas id="canvasBarrage" class="canvas-barrage"></canvas>
      <div class="video-placeholder"></div>
      <div id="lottiePlayGround" class="lottie-play-ground"></div>
    </div>

    <div class="input-wrap">
      <input type="text" v-model="barrage" />
      <button @click="send">发送</button>
      <button @click="play">播放</button>
    </div>
    <div class="input-wrap">
      <button @click="effect(1)">特效1</button>
      <button @click="effect(2)">特效2</button>
    </div>
  </div>
</template>

<script>
import lottie from "lottie-web";
import canvasBarrage from "@/tools/canvasBarrage";
// 弹幕数据
var dataBarrage = [
  {
    value: "speed设为0为非滚动",
    speed: 0,
  },
  {
    value: "time控制弹幕时间，单位秒",
    color: "blue",
  },
  {
    value: "视频共21秒",
  },
  {
    value: "视频背景为白色",
  },
  {
    value: "视频为录制",
  },
  {
    value: "视频内容简单",
  },
  {
    value: "是为了让视频尺寸不至于过大",
  },
  {
    value: "省流量",
  },
  {
    value: "支持弹幕暂停（视频暂停）",
  },
  {
    value: "add()方法新增弹幕",
  },
  {
    value: "reset()方法重置弹幕",
  },
  {
    value: "颜色，字号，透明度可全局设置",
  },
  {
    value: "具体交互细节可参考页面源代码",
  },
  {
    value: "内容不错哦！",
    color: "yellow",
  },
];
let demoBarrage = null;
export default {
  name: "Home",
  data() {
    return {
      barrage: "",
      canvasBarrage: null,
      myLottie: null,
    };
  },
  mounted() {
    let nowTime = new Date();
    dataBarrage.forEach((item, index) => {
      item.time = nowTime.setTime(nowTime.getTime() + index * 200);
    });
    // console.log(dataBarrage);
    this.canvasBarrage = new canvasBarrage("#canvasBarrage", { data: dataBarrage });
    // this.canvasBarrage.play();
  },
  methods: {
    effect(type) {
      if (this.myLottie && !this.isAnimeFinished) {
        this.myLottie.destroy();
        this.isAnimeFinished = true;
      }
      console.log(type);
      this.isAnimeFinished = false;
      this.myLottie = lottie.loadAnimation({
        container: document.getElementById("lottiePlayGround"), // the dom element that will contain the animation
        renderer: "canvas",
        loop: false,
        autoplay: true,
        path: `./lottie/${type}.json`, // the path to the animation json
      });
      this.myLottie.onComplete = () => {
        console.log("complete");
        this.myLottie.destroy();
        this.isAnimeFinished = true;
      };
      this.myLottie.onde;
      this.myLottie.play();
    },
    send() {
      this.canvasBarrage.add({
        value: this.barrage,
        time: new Date().getTime(),
      });
      this.barrage = "";
    },
    play() {
      this.canvasBarrage.play();
    },
  },
};
</script>
<style lang="css" scoped>
.video-x {
  position: relative;
  width: 640px;
  margin: auto;
}

.canvas-barrage {
  position: absolute;
  width: 640px;
  height: 360px;
  top: 0;
  left: 0;
  z-index: 2;
}
.lottie-play-ground {
  position: absolute;
  width: 640px;
  height: 360px;
  top: 0;
  left: 0;
  z-index: 1;
}
.video-placeholder {
  height: 360px;
  background-color: #000;
  animation: bgColor 10s infinite alternate;
}
button {
  margin: 10px;
}
@keyframes bgColor {
  25% {
    background-color: darkred;
  }
  50% {
    background-color: darkgreen;
  }
  75% {
    background-color: darkblue;
  }
  100% {
    background-color: sliver;
  }
}
</style>
