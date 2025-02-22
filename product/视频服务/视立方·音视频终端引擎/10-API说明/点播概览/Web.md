
本文档是介绍适用于点播播放的 Web 超级播放器（ TCPlayer ）的相关参数以及 API，需结合 [超级播放器](https://cloud.tencent.com/document/product/1449/57088) 使用。本文档适合有一定 Javascript 语言基础的开发人员阅读。

## 初始化参数
播放器初始化需要传入两个参数，第一个为播放器容器 ID，第二个为功能参数对象。
```
var player = TCPlayer('player-container-id', options);
```

### options 参数列表
options 对象可配置的参数：

| 名称    | 类型                      | 默认值                        |说明 |
|------------|-----------------------------------|-----------------------------------|---------------------------------------|
|  appID|  String |   无 |必选。|
|  fileID|  String|无|必选。|  
|  width|  String/Number|  无| 播放器区域宽度，单位像素，按需设置，可通过 CSS 控制播放器尺寸。|
|  height |  String/Number|  无|  播放器区域高度，单位像素，按需设置，可通过 CSS 控制播放器尺寸。|  
|  controls|  Boolean|  true|  是否显示播放器的控制栏。|  
|  poster|  String|  无|  设置封面图片完整地址（如果上传的视频已生成封面图，优先使用生成的封面图，详细请参见 [云点播 - 管理视频](https://cloud.tencent.com/document/product/266/36452)）。|  
|  autoplay|  Boolean|  false|  是否自动播放。|  
|  playbackRates|  Array| [0.5，1，1.25，1.5，2]|  设置变速播放倍率选项，仅 HTML5 播放模式有效。|  
|  loop|Boolean|  false|  是否循环播放。|  
|  muted|  Boolean|  false|  是否静音播放。|  
|  preload|  String|  auto|  是否需要预加载，有3个属性"auto"，"meta"和"none" ，移动端由于系统限制，设置 auto 无效。|  
|  swf|  String|  无|  Flash 播放器 swf 文件的 URL。|  
|  posterImage|  Boolean|  true|  是否显示封面。|  
|  bigPlayButton|  Boolean|  true|  是否显示居中的播放按钮（浏览器劫持嵌入的播放按钮无法去除）。|  
|  language|  String|  "zh-CN"|  设置语言。|  
|  languages|  Object|  无|  设置多语言词典。|  
|  controlBar|  Object|  无|  设置控制栏属性的参数组合，后面有详细介绍。|  
|  plugins|  Object|  无|  设置插件功能属性的参数组合，后面有详细介绍。|  
|  hlsConfig|  Object|  无|  hls.js 的启动配置，详细内容请参见官方文档 [hls.js](https://github.com/video-dev/hls.js/blob/master/docs/API.md#fine-tuning)。|  

>! controls、playbackRates、loop、preload、posterImage 这些参数在浏览器劫持播放的状态下将无效（[什么是劫持播放？](https://cloud.tencent.com/document/product/881/20219#.E6.B5.8F.E8.A7.88.E5.99.A8.E5.8A.AB.E6.8C.81.E8.A7.86.E9.A2.91.E6.92.AD.E6.94.BE)）。

#### controlBar 参数列表
controlBar 参数可以配置播放器控制栏的功能，支持的属性有：

| 名称    | 类型                      | 默认值                        |说明 |
|------------|-----------------------------------|-----------------------------------|---------------------------------------|
|  playToggle| Boolean|  true|  是否显示播放、暂停切换按钮。|  
|  progressControl|  Boolean| true|  是否显示播放进度条。|  
|  volumePanel|  Boolean|  true|  是否显示音量控制。|  
|  currentTimeDisplay|  Boolean|  true|  是否显示视频当前时间。|  
|  durationDisplay|  Boolean|  true|  是否显示视频时长。|  
|  timeDivider|  Boolean|  true|  是否显示时间分割符。|  
|  playbackRateMenuButton|  Boolean|  true|  是否显示播放速率选择按钮。|  
|  fullscreenToggle|  Boolean|  true|  是否显示全屏按钮。|  
|  QualitySwitcherMenuButton|  Boolean|  true|  是否显示清晰度切换菜单。|  

>! controlBar 参数在浏览器劫持播放的状态下将无效（[什么是劫持播放？](https://cloud.tencent.com/document/product/881/20219#.E6.B5.8F.E8.A7.88.E5.99.A8.E5.8A.AB.E6.8C.81.E8.A7.86.E9.A2.91.E6.92.AD.E6.94.BE)）。

#### plugins 插件参数列表
plugins 参数可以配置播放器插件的功能，支持的属性有：

| 名称    | 类型                      | 默认值                        |说明 |
|------------|-----------------------------------|-----------------------------------|---------------------------------------|
|  ContinuePlay|  Object|  无|  控制续播功能，支持的属性如下：<br><li>auto：false（是否在播放时自动续播）。<br><li>text：“上次看到”（提示文案）。<br><li>btnText：“恢复播放”（按钮文案）。<br>

## 对象方法
初始化播放器返回对象的方法列表：

| 名称    | 参数及类型                 | 返回值及类型                        |说明 |
|------------|-----------------------------------|-----------------------------------|---------------------------------------|
|  ready(function)|  (Function)|  无|  设置播放器初始化完成后的回调。|  
|  play()|  无|  无|  播放以及恢复播放。|  
|  pause()|  无|  无|  暂停播放。|  
|  currentTime(seconds)|  (Number)|  (Number)|  获取当前播放时间点，或者设置播放时间点，该时间点不能超过视频时长。|  
|  duration()|  无|  (Number)|  获取视频时长。|  
|  volume(percent)|  (Number)[0，1][可选]|  (Number)/设置时无返回|  获取或设置播放器音量。|
|  poster(src)|  (String)|  (String)/设置时无返回|  获取或设置播放器封面。|
|  requestFullscreen()|  无|  无|  进入全屏模式。|  
|  exitFullscreen()|  无|  无|  退出全屏模式。|  
|  isFullscreen()|  无|  Boolean|  返回是否进入了全屏模式。|  
|  on(type，listener)|  (String, Function)|  无|  监听事件。|  
|  one(type，listener)|  (String, Function)|  无|  监听事件，事件处理函数最多只执行1次。|  
|  off(type，listener)|  (String, Function)|  无|  解绑事件监听。|  
|  buffered()|  无|  TimeRanges|  返回视频缓冲区间。|  
|  bufferedPercent()|  无|  值范围[0，1]|  返回缓冲长度占视频时长的百分比。|  
|  width()|  (Number)[可选]|  (Number)/设置时无返回|  获取或设置播放器区域宽度，如果通过 CSS 设置播放器尺寸，该方法将无效。|
|  height()|  (Number)[可选]|  (Number)/设置时无返回|  获取或设置播放器区域高度，如果通过 CSS 设置播放器尺寸，该方法将无效。|
|  videoWidth()|  无|  (Number)|  获取视频分辨率的宽度。|  
|  videoHeight()|  无|  (Number)|  获取视频分辨率的高度。|  
|  dispose()|  无|  无|  销毁播放器。|  

>! 对象方法不能同步调用，需要在相应的事件（如 loadedmetadata）触发后才可以调用，除了 ready、on、one 以及 off。

## 事件
播放器可以通过初始化返回的对象进行事件监听，示例：
```
var player = TCPlayer('player-container-id', options);
// player.on(type, function);
player.on('error', function(error) {
   // 做一些处理
});
```
其中 type 为事件类型，支持的事件有：

| 名称    | 介绍                    |  
|------------|---------------------------------|
|  play|  已经开始播放，调用 play() 方法或者设置了 autoplay 为 true 且生效时触发，这时 paused 属性为 false。|  
|  playing|  因缓冲而暂停或停止后恢复播放时触发，paused 属性为 false 。通常用这个事件来标记视频真正播放，play 事件只是开始播放，画面并没有开始渲染。|  
|  loadstart|  开始加载数据时触发。|  
|  durationchange|  视频的时长数据发生变化时触发。|  
|  loadedmetadata|  已加载视频的 metadata。|  
|  loadeddata|  当前帧的数据已加载，但没有足够的数据来播放视频的下一帧时，触发该事件。|  
|  progress|  在获取到媒体数据时触发。|  
|  canplay|  当播放器能够开始播放视频时触发。|  
|  canplaythrough|  当播放器预计能够在不停下来进行缓冲的情况下持续播放指定的视频时触发。|
|  error|  视频播放出现错误时触发。|  
|  pause|  暂停时触发。|  
|  ratechange|  播放速率变更时触发。|  
|  seeked|  搜寻指定播放位置结束时触发。|  
|  seeking|  搜寻指定播放位置开始时触发。|  
|  timeupdate|  当前播放位置有变更，可以理解为 currentTime 有变更。|  
|  volumechange|  设置音量或者 muted 属性值变更时触发。|  
|  waiting|  播放停止，下一帧内容不可用时触发。|  
|  ended|  视频播放已结束时触发。此时 currentTime 值等于媒体资源最大值。|  
|  resolutionswitching|  清晰度切换进行中。|  
|  resolutionswitched|  清晰度切换完毕。|  
|  fullscreenchange| 全屏状态切换时触发。|

## 错误码
当播放器触发 error 事件时，监听函数会返回错误码，其中3位数以上的错误码为媒体数据接口错误码。错误码列表：

| 名称 | 描述                                           |
|------|----------------------------------------------|
| -1   | 播放器没有检测到可用的视频地址。                  |
| -2   | 获取视频数据超时。                               |
| 1    | 视频数据加载过程中被中断。<br>可能原因：<br><li> 网络中断。<br><li> 浏览器异常中断。<br>解决方案：<br><li> 查看浏览器控制台网络请求信息，确认网络请求是否正常。<br><li>重新进行播放流程。                             |
| 2    | 由于网络问题造成加载视频失败。<br>可能原因：网络中断。<br>解决方案:<br><li> 查看浏览器控制台网络请求信息，确认网络请求是否正常。<br><li> 重新进行播放流程。                     |
| 3    | 视频解码时发生错误。<br>可能原因：视频数据异常，解码器解码失败。<br>解决方案：<br><li> 尝试重新转码再进行播放，排除由于转码流程引入的问题。<br><li> 确认原始视频是否正常。 <br><li> 请联系技术客服并提供播放参数进行定位排查。                                |
| 4    | 视频因格式不支持或者服务器或网络的问题无法加载。<br>可能原因：<br><li> 获取不到视频数据，CDN 资源不存在或者没有返回视频数据。<br><li> 当前播放环境不支持播放该视频格式。<br>解决方案：<br><li> 查看浏览器控制台网络请求信息，确认视频数据请求是否正常。<br><li> 确认是否按照使用文档加载了对应视频格式的播放脚本。<br><li> 确认当前浏览器和页面环境是否支持将要播放的视频格式。 <br><li> 请联系技术客服并提供播放参数进行定位排查。     |
| 5    | 视频解密时发生错误。<br>可能原因：<br><li> 解密用的密钥不正确。<br><li> 请求密钥接口返回异常。<br><li> 当前播放环境不支持视频解密功能。<br>解决方案：<br><li> 确认密钥是否正确，以及密钥接口是否返回正常。<br><li> 请联系技术客服并提供播放参数进行定位排查。<br>                                  |
| 10   | 点播媒体数据接口请求超时。在获取媒体数据时，播放器重试3次后仍没有任何响应，会抛出该错误。<br>可能原因：<br><li> 当前网络环境无法连接到媒体数据接口，或者媒体数据接口被劫持。<br><li> 媒体数据接口异常。<br>解决方案：<br><li> 尝试打开我们提供的 Demo 页面看是否可以正常播放。 <br><li>请联系技术客服并提供播放参数进行定位排查。<br>                           |
| 11   | 点播媒体数据接口没有返回数据。在获取媒体数据时，播放器重试3次后仍没有数据返回，会抛出该错误。<br>可能原因：<br><li> 当前网络环境无法连接到媒体数据接口，或者媒体数据接口被劫持。<br><li> 媒体数据接口异常。<br>解决方案：<br><li> 尝试打开我们提供的 Demo 页面看是否可以正常播放。 <br><li> 请联系技术客服并提供播放参数进行定位排查。<br>                        |
| 12   | 点播媒体数据接口返回异常数据。在获取媒体数据时，播放器重试3次后仍返回无法解析的数据，会抛出该错误。<br>可能原因：<br><li> 当前网络环境无法连接到媒体数据接口，或者媒体数据接口被劫持。<br><li> 播放参数有误，媒体数据接口无法处理。<br><li> 媒体数据接口异常。 <br>解决方案：<br><li> 尝试打开我们提供的 Demo 页面看是否可以正常播放。 <br><li> 请联系技术客服并提供播放参数进行定位排查。<br>                   |
| 13   | 播放器没有检测到可以在当前播放器播放的视频数据，请对该视频进行转码操作。 |
| 14   | HTML5 + hls.js 模式下播放 hls 出现网络异常，异常详情可在 event.source 中查看，详细介绍请看 hls.js 的官方文档 [Network Errors](https://github.com/video-dev/hls.js/blob/master/docs/API.md#network-errors)。 |
| 15   | HTML5 + hls.js 模式下播放 hls 出现多媒体异常，异常详情可在 event.source 中查看，详细介绍请看 hls.js 的官方文档 [Media Errors](https://github.com/video-dev/hls.js/blob/master/docs/API.md#media-errors)。   |
| 16   | HTML5 + hls.js 模式下播放 hls 出现多路复用异常，异常详情可在 event.source 中查看，详细介绍请看 hls.js 的官方文档 [Mux Errors](https://github.com/video-dev/hls.js/blob/master/docs/API.md#mux-errors)。     |
| 17   | HTML5 + hls.js 模式下播放 hls 出现其他异常，异常详情可在 event.source 中查看，详细介绍请看 hls.js 的官方文档 [Other Errors](https://github.com/video-dev/hls.js/blob/master/docs/API.md#other-errors)。     |
| 10008| 媒体数据服务没有找到对应播放参数的媒体数据，请确认请求参数 appID fileID 是否正确，以及对应的媒体数据是否已经被删除。 |

