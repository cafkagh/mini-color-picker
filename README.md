# mini-color-picker

> 小程序拾色器（颜色选择器）组件,通过调色盘取色，用于用户自定义场景。

[![](https://img.shields.io/npm/v/mini-color-picker.svg)](https://www.npmjs.com/package/mini-color-picker/)

**对比**:

- [we-color-picker](https://github.com/KirisakiAria/we-color-picker)
需注意组件定位，操作[不跟手不流畅](https://developers.weixin.qq.com/community/develop/doc/00084ae5e400a8ae58e78263553c06#0006ae9d7c0ea05fe298cc59e514),配置复杂。其定位会撑开原有页面，体验不佳。滑动距离按像素区分(固定)，需考虑设备分辨率，不利于多端。
- [PapaerPen](https://www.jianshu.com/p/989b580168cd)
利用原有slider组件实现滑动选取，不限于设备分辨率。但需三次操作。

**特性**:

本组件利用官方提供的slider实现选择色相，movable-view选择饱和度和明度，由于是官方基础组件，操作顺畅。在滑动区域的设定上，使用占比来影响色值变化，无需考虑rpx转换。在操作流程上，限于手机操作区域，不能使用Popover，使用底部拉起弹窗，不影响原有页面，[重点突出](https://developers.weixin.qq.com/miniprogram/design/#%E9%87%8D%E7%82%B9%E7%AA%81%E5%87%BA)。在操作预览上，由于弹窗遮罩不可避免无法实时预览，采用色相滑块的颜色来实现预览。同时考虑了iphone-x的安全区域问题。

## 使用效果
### 截图

![mini-color-picker](https://imgkr.cn-bj.ufileos.com/b136c18d-9142-4476-8779-cb0a34fa7bef.png)
![mini-color-picker](https://imgkr.cn-bj.ufileos.com/dcb57311-2305-4f47-b8f8-4cdf3e824c9e.gif)

### 样例

[在开发者工具中预览效果](https://developers.weixin.qq.com/s/GcP4LBmv77h6)=>代码片段ID:`GcP4LBmv77h6`

![mini-program-demo](https://imgkr.cn-bj.ufileos.com/f04ae7f1-8a28-4761-acb4-db25616f55b2.png)
## 安装使用
### 1. 获取组件
#### git
可能不稳定，但包含最新功能更新
```sh
git clone https://github.com/MakerGYT/mini-color-picker.git
```
将项目中components/color-picker文件夹拷贝到组件路径下
#### npm
稳定
```sh
npm install mini-color-picker --save
```
使用npm包请参考[微信小程序官方文档](https://developers.weixin.qq.com/miniprogram/dev/devtools/npm.html)

### 2. 引入组件
在使用该组件的页面对应json文件中添加：
```json
{
  "usingComponents": {
    "color-picker":"/components/color-picker/color-picker" 
  }
}
```
如使用npm,
点击开发者工具中的菜单栏：工具 --> 构建 npm;
勾选“使用 npm 模块”选项
```json
{
  "usingComponents": {
    "color-picker":"mini-color-picker/color-picker" 
  }
}
```

### 3. 使用组件
参考[/pages](https://github.com/makergyt/mini-color-picker/tree/master/demo/pages/index)
```html
<!-- index.wxml -->
<view style="background:{{rgb}};width:100px;height:24px;" bindtap="toPick"></view>
<color-picker bindchangeColor="pickColor" initColor="{{rgb}}" show="{{pick}}" />
```
```js
Page({
  data:{
    rgb: 'rgb(0,154,97)',//初始值
    pick: false
  },
  // 显示取色器
  toPick: function () {
    this.setData({
      pick: true
    })
  },
  //取色结果回调
  pickColor(e) {
    let rgb = e.detail.color;
  },
}) 
```
## 属性列表
| 属性 |类型| 默认值|必填|说明|
| -- | --|--|--|--|
| show | Boolean | false | 是 |是否显示 |
|initColor| String | rgb(255,0,0)| 是　|初始色,rgb表示|
|mask | Boolean |true | 否 |是否显示背景蒙层|
|maskClosable | Boolean | true | 否 |点击背景蒙层是否可以关闭 |
|bindchangeColor|eventhandler| | 否 | 取色后的回调,event.detail = {color} |
|bindclose|eventhandler||否| 点击背景蒙层关闭掉color-picker后触发的事件|

**注意**:

外部与组件通信的数据格式是rgb,为了避免引入多种数据格式而导致实际场景代码冗余，开发者可自行按需转换，在公众号"MakerGYT"回复以下对应内容获取参考函数代码:
- rgb2hex
- rgb2hsv
- rgb2cmyk
- hex2rgb
- hsv2rgb

![MakerGYT公众号](https://cdn.blog.makergyt.com/images/landmark-wechat_official-qrcode.jpg)

## License
[MIT](https://github.com/MakerGYT/mini-color-picker/blob/master/LICENSE) © MakerGYT