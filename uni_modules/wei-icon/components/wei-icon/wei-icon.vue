<template>
  <view class="wei-icon-wrapper">
    <image v-if="isImage" :src="name" :style="imageStyle"></image>
    <text v-else class="wei-icon" :style="iconStyle">{{iconName}}</text>
    <view 
      v-if="isBadge" 
      :class="[dot ? 'wei-icon-badge-dot' : 'wei-icon-badge']"
      :style="badgeStyle"
    >
      <text class="badge-text" v-if="!dot && badge">{{ getBadgeContent }}</text>
    </view>
  </view>
</template>
<script>
  // 引入图标名称，已经对应的unicode
  import icons from './icons.js';
  // #ifdef APP-NVUE
  var domModule = weex.requireModule('dom');
  import iconUrl from './weiicons.ttf'
  domModule.addRule('fontFace', {
    'fontFamily': "weiicons",
    'src': "url('" + iconUrl + "')"
  });
  // #endif
  
  function getUnit(value) {
    return !isNaN(value) ? `${value}px` : value;
  }
  
  /**
   * @property {String} name 图标名称或图片链接
   * @property {String} color 图标颜色 默认 #323233
   * @property {String|Number} size 图标大小，如 20px 40rpx，默认单位为 px
   * @property {String} classPrefix 类名前缀，用于使用自定义图标
   * @property {Boolean} dot 是否显示图标右上角小红点 默认false
   * @property {String|Number} badge 图标右上角徽标的内容
   * @property {String} badgePosition = [top-right|top-left|bottom-left|bottom-right] 徽标位置 默认 top-right
   * @property {String} badgeMax 最大值，超过最大值会显示 {max}+，仅当 badge 为数字时有效
   * @property {Boolean} badgeShowZero 当 badge 为数字 0 或字符串 '0' 时，是否展示徽标 默认 true
   * @property {Array} badgeOffset 设置徽标的偏移量，数组的两项分别对应水平向右和垂直向下方向的偏移量，默认单位为 px
   * @property {String} badgeColor 徽标背景颜色 默认 #ee0a24
   */
  export default {
    props: {
      name: {
        type: String,
        required: true,
      },
      color: {
        type: String,
        default: '#323233'
      },
      size: {
        type: [String, Number],
        default: 32,
      },
      classPrefix: {
        type: String,
        default: null,
      },
      dot: {
        type: Boolean,
        default: false,
      },
      badge: {
        type: [Number, String],
        default: null,
      },
      badgePosition: {
        type: String,
        default: 'top-right'
      },
      badgeMax: {
        type: [String, Number],
        default: null,
      },
      badgeShowZero: {
        type: Boolean,
        default: true,
      },
      badgeOffset: {
        type: Array,
        default: null,
      },
      badgeColor: {
        type: String,
        default: "#ee0a24"
      },
    },
    data: () => ({}),
    computed: {
      iconStyle() {
        let style = `font-size:${getUnit(this.size)};line-height:${getUnit(this.size)};`;
        if(this.color) {
          style += `color:${this.color};`;
        }
        return style;
      },
      isImage() {
        if(this.name.indexOf('/') >= 0) 
          return true;
        return false;
      },
      isBadge() {
        if(this.dot || (this.badge && this.badge !== '')) {
          //如果为0,不展示徽标
          if(!this.badgeShowZero && (this.badge === 0 || this.badge === '0')) {
            return false;
          }
          return true;
        }
        return false;
      },
      iconName() {
        const prefix = !!this.classPrefix ? this.classPrefix : 'weiicon-';
        return icons[prefix + this.name] || this.name;
      },
      imageStyle() {
        let style = '';
        if(this.size) {
          style += `width:${getUnit(this.size)};height:${getUnit(this.size)};`
        }
        return style;
      },
      getBadgeContent() {
        if((this.badgeMax && !isNaN(this.badgeMax)) 
          && (this.badge && !isNaN(this.badge)) 
          && parseInt(this.badge) > parseInt(this.badgeMax)) {
          return this.badgeMax + '+';
        }
        return this.badge;
      },
      badgeStyle() {
        let style = '';
        if(this.badgePosition === 'top-left') {
          style += `top:0;left:0;`;
          // #ifndef APP-NVUE
          style += 'transform:translate(-50%, -50%);'
          // #endif
        } else if(this.badgePosition === 'bottom-left') {
          style += `bottom:0;left:0;`;
          // #ifndef APP-NVUE
          style += 'transform:translate(-50%, 50%);'
          // #endif
        } else if(this.badgePosition === 'bottom-right') {
          style += `bottom:0;right:0;`;
          // #ifndef APP-NVUE
          style += 'transform:translate(50%, 50%);'
          // #endif
        } else {
          style += `top:0;right:0;`;
          // #ifndef APP-NVUE
          style += 'transform:translate(50%, -50%);'
          // #endif
        }
        return style;
      }
    },
  }
</script>
<style>
  /* #ifndef APP-NVUE */
  @import './weiicons.css';
  /* #endif */
  .wei-icon-wrapper {
    position: relative;
  }
  .wei-icon {
    font-family: weiicons;
  }
  .wei-icon-badge {
    position: absolute;
    background-color: #ee0a24;
    /* #ifndef APP-NVUE */
    min-width: 16px;
    /* #endif */
    font-size: 12px;
    line-height: 1.2;
    text-align: center;
    border: 1px solid #fff;
    border-radius: 999px;
    padding: 0 3px;
  }
  .wei-icon-badge .badge-text {
    color: #fff;
  }
  .wei-icon-badge-dot {
    position: absolute;
    width: 8px;
    height: 8px;
    border-radius: 50%;
    background-color: #ee0a24;
  }
</style>
