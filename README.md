# Vue-AliPlayer

> A Vue 2.x video player component based on [vue-aliplayer](https://github.com/slacrey/vue-aliplayer).


## Install

```bash
npm install vue-aliplayer -S
```

## Usage

```js
import VueAliplayer from 'vue-aliplayer'

export default {
  components: {
    'ali-player': VueAliplayer
  }
}
```
## Props

| 名称    | 类型 | 默认值 | 说明 |
| ---------- | ---- | ------- | ----------- |
| aliplayerSdkPath | String | //g.alicdn.com/de/prismplayer/2.1.0/aliplayer-min.js | 阿里播放器引用地址 |
| playStyle | String |  | 播放器自定义样式style |
| source | String |  | 视频播放地址url：1、单独url；2、默认状态，表示使用“vi+playauth3、source播放方式优先级最高 |
| vid | String |  | 媒体转码服务的媒体Id |
| playauth | String |  | 播放权证，如何得到可参考：获取[playauth](https://help.aliyun.com/document_detail/52833.html?spm=5176.doc51236.6.627.5gm5gf) |
| height | String | 100% | 播放器高度，可形如’100%’或者’100px’ |
| width | String | 320px | 播放器宽度，可形如’100%’或者’100px’ |
| cover | String |  | 播放器默认封面图片，请填写正确的图片url地址Flash播放器封面也需要[开启允许跨域访问](https://player.alicdn.com/aliplayer/docs/blogs/how-to-handle-flash-crossdomain.html) |
| isLive | Boolean | false | 播放内容是否为直播，直播时会禁止用户拖动进度条 |
| autoplay | Boolean | false | 播放器是否自动播放，在移动端autoplay属性会失效 |
| useH5Prism | Boolean | false | 指定使用H5播放器 |
| useFlashPrism | Boolean | false | 指定使用Flash播放器 |
| playsinline | Boolean | false | H5是否内置播放，有的Android浏览器不起作用 |
| format | String | mp4 | 指定播放地址格式，只有使用vid+plauth播放方式时支持可选值为'mp4'和'm3u8',默认为'mp4' |
| x5-type | String | 'auto' | 声明启用同层H5播放器，启用时设置的值为'h5'具体参考[同层播放](https://player.alicdn.com/aliplayer/docs/blogs/how-to-handle-h5-same-layer.html) |
| x5_fullscreen | Boolean | false |声明视频播放时是否进入到TBS的全屏模式，默认为false具体参考[同层播放](https://player.alicdn.com/aliplayer/docs/blogs/how-to-handle-h5-same-layer.html) |
| x5_video_position | String | center | 声明视频播在界面上的位置，默认为"center" 可选值为：'top'，'center' 具体参考[同层播放](https://player.alicdn.com/aliplayer/docs/blogs/how-to-handle-h5-same-layer.html) |
| x5_orientation| String |  | 声明TBS播放器支持的方向，可选值：landscape:横屏） portraint:竖屏 landscape |
| autoPlayDelay| Number |  | 延迟播放时间，单位为秒具体参考[延迟播放](https://player.alicdn.com/aliplayer/docs/blogs/how-to-implementment-delay-play.html) |
| autoPlayDelayDisplayText| String |  | 延迟播放提示文本具体参考[延迟播放](https://player.alicdn.com/aliplayer/docs/blogs/how-to-implementment-delay-play.html) |


## Method

| 名称 | 参数 | 描述 |
| ---- | ------ | ----------- |
| play | none | 播放视频 |
| pause | none | 暂停视频 |
| replay | none | 重播视频 |
| seek | time | 跳转到某个时刻进行播放，time的单位为秒 |
| getCurrentTime | none | 获取当前的播放时刻，返回的单位为秒 |
| getDuration | none | 获取视频总时长，返回的单位为秒 |
| getVolume | none | 获取当前的音量，返回值为0-1的实数ios和部分android会失效 |
| setVolume | vol | 设置音量，vol为0-1的实数，ios和部分android会失效 |
| loadByUrl | url,time | 直接播放视频url，time为可选值（单位秒）目前只支持同种格式（mp4/flv/m3u8）之间切换,暂不支持直播rtmp流切换 |
| reloaduserPlayInfoAndVidRequestMts | vid：视频id playauth：播放凭证 | 目前只支持HTML5界面上的重载功能，暂不支持直播rtmp流切换m3u8）之间切换，暂不支持直播rtmp流切换 |
| setPlayerSize | w,h | 设置播放器大小w,h可分别为400px像素或60%百分比chrome浏览器下flash播放器分别不能小于397x297 |
| setSpeed | speed | 设置倍速播放移动端可能会失效，比如android 微信 |

## Events

| 名称 | 参数 | 描述 |
| ---- | ------ | ----------- |
| ready | none | Triggered when aliplayer is ready |
| play | none | Triggered when aliplayer start play |
| pause | none | Triggered when aliplayer paused |
| waiting | none | Triggered periodically when aliplayer is waiting |
| ended | none | Triggered when aliplayer ended playing |
| liveStreamStop | none | Triggered when live stream is stop |
| hideBar | none | Triggered when control bar is hide |

Example:

```js
<ali-player @play="play"></ali-player>

export default {
    methods: {
      play() {
        console.log('play callback')
      }
    }
```

## API

you can use all aliplayer api

Example:

```js
<ali-player :source="视频url" :vid="视频vid" :playauth="播放鉴权" ref="player"></ali-player>
    <button @click="play">播放</button>
    <button @click="pause">暂停</button>
    <button @click="replay">重播</button>

export default {
    methods: {
      play: function(){
        const player = this.$refs.player.instance
        player && player.play()
      },
      pause: function() {
        const player = this.$refs.player.instance
        player && player.pause()
      },
      replay: function() {
        const player = this.$refs.player.instance
        player && player.replay()
      }
    }
```

## Development

- `yarn dev`: Run dev in development mode
- `yarn deploy`: Deploy dev to gh-pages
- `yarn build:cjs`: Build component in commonjs format
- `yarn build:umd`: Build component in umd format
- `yarn build`: Build component in both format
- `yarn lint`: Run eslint

Check out your npm scripts, it's using [vbuild](https://github.com/egoist/vbuild) under the hood.

---


# License

This content is released under the [MIT](http://opensource.org/licenses/MIT) License.
