# barrage-demo

> 基于张鑫旭的[使用canvas实现和HTML5 video交互的弹幕效果](http://www.zhangxinxu.com/wordpress/?p=6386)源码改造


## 效果
![image](http://github.com/ft3590782/barrage-demo/demo.gif)

### Project setup
```
yarn install
```

### Compiles and hot-reloads for development
```
yarn serve
```

### Compiles and minifies for production
```
yarn build
```

### 区别
去掉了与视频的绑定,根据自然时间来推送弹幕进度,比较适合年会现场等大屏静态互动场景,支持vue直接使用

### 使用方式
引入canvasBarrage.js

```javascript
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
  ...
];
```

处理数据,这里是为了展示效果根据当前时间造假数据的时间
```javascript
  mounted() {
    let nowTime = new Date();
    dataBarrage.forEach((item, index) => {
      item.time = nowTime.setTime(nowTime.getTime() + index * 200);
    });
    //创建实例
    this.canvasBarrage = new canvasBarrage("#canvasBarrage", { data: dataBarrage });
    //mounted之后立即播放
    this.canvasBarrage.play();
  }
```

完整源码可以看github,github上的demo还结合了lottie效果做了特效

### License

MIT