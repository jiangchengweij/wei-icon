# 快速使用的图标库

从vant搬运过来的图标，个人觉得它比uni-icons更易于移动端使用，支持nvue和显示徽标

#### 为什么要开发这个图标库，不直接使用vant或其他UI框架的图标呢？

首先vant并不支持在uni-app直接使用，其次当你想使用图标的时候可以单独直接应用这个图标库组件，
而不需要把UI库都引入进来

### 使用示例

```
<wei-icon name="chat-o"></wei-icon>
<wei-icon name="chat-o" :badge="9"></wei-icon>
```

图标name名称可以直接参考[vant](http://vant-contrib.gitee.io/vant/#/zh-CN/icon)

#### 属性说明

|属性名	           |类型	      |默认值	|说明	  |
|:--:|:--:|:--:|:--:|
|name              |String    |null     |图标名称或图片链接|
|color             |String    |#323233  |图标颜色 ，16进制|
|size              |String-Number   |32  |图标大小，如 20px 40rpx，默认单位为 px|
|classPrefix       |String    |  |类名前缀，用于使用自定义图标|
|dot               |Boolean   |false  |是否显示图标右上角小红点|
|badge             |String-Number    |  |图标右上角徽标的内容|
|badgePosition     |String   |top-right  | 徽标位置 默认 top-right,支持top-right,top-left,bottom-left,bottom-right |
|badgeMax          |String   |     |最大值，超过最大值会显示 {max}+，仅当 badge 为数字时有效|
|badgeShowZero     |String   |     |当 badge 为数字 0 或字符串 '0' 时，是否展示徽标 默认 true|
|badgeOffset       |String   |     |设置徽标的偏移量，数组的两项分别对应水平向右和垂直向下方向的偏移量，默认单位为 px|
|badgeColor        |String |#ee0a24   |徽标背景颜色

如果觉得解决了你的图标使用问题，方便给个小小的star吗。[github](https://github.com/jiangchengweij/wei-icon)

