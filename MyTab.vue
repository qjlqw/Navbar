<template>
  <view :class="{ fixed: fixed }">
    <view
      :class="`titleBar ${top > 0 ? 'height-2' : 'height-1'}`"
      :style="{ background: background, color: color }"
    >
      <view class="text">{{ title }}</view>
    </view>

    <!-- <view 
      v-if="showReturn"
      :class="`returnBtn-public ${ top == 0 ? 'top-1' : 'top-2' }`" 
      @tap='ifBack'
    >
      <text class="icon-arrow-left iconfont" :style="{ color: color }" ></text>
    </view> -->

    <navigator 
      hover-class="none" 
      :open-type="openType" 
      :url="url"
      :delta="delta"
    >
      <view
        class="returnBtn"
        :class="`returnBtn-public ${top == 0 ? 'top-1' : 'top-2'}`"
      >
        <text
          v-if="backBtntype==0"
          :class="`iconfont ${backBtn == true ? 'icon-arrow-left' : ''}`"
          :style="{ color: backBtnColor }"
        ></text>
        <image v-else src="../assets/index.png"></image>
      </view>
    </navigator>
  </view>
</template>

<script>
import Taro from "@tarojs/taro";

export default {
  /**
   * title        页面标题
   * background   背景颜色
   * color        字体颜色
   * showReturn   是否展示返回按钮
   * jump         是否跳转 默认为false, 如为true则会有点击事件
   * operateType  自定义跳转方式
   * fixed        是否是绝对定位 默认为false
   * openType     跳转类型
   * backBtn      是否展示返回按钮
   * delta        open-type为'navigateBack'时有效，表示回退的层数
   * backBtntype  是箭头返回还是那种类型的返回
   */
  props: {
    title: {
      type: String,
    },
    background: {
      type: String,
      default: "#FE724C",
    },
    color: {
      type: String,
      default: "#FFFFFF",
    },
    showReturn: {
      type: Boolean,
      default: false,
    },
    jump: {
      type: Boolean,
      default: false,
    },
    fixed: {
      type: Boolean,
      default: false,
    },
    url: {
      type: String,
      default: "/pages/realTime/index",
    },
    openType: {
      type: String,
      default: "navigateBack",
    },
    backBtn: {
      type: Boolean,
      default: true,
    },
    delta: {
      type: Number,
      default: 1,
    },
    backBtnColor: {
      type: String,
      default: "#FFFFFF",
    },
    backBtntype: {
      type: Number,
      default:0
    }
  },

  data() {
    return {
      top: this.$store.state.top,
    };
  },

  methods: {
    ifBack() {
      if (this.url) {
        Taro.reLaunch({ url: this.url });
      } else if (this.jump) this.$emit("back");
      else Taro.navigateBack({ delta: 1 });
    },
  },
};
</script>

<style lang='less'>
@font-face {
  font-family: "iconfont";
  src: url("//at.alicdn.com/t/font_2355444_eortiv1scql.eot?t=1611887868038"); /* IE9 */
  src: url("//at.alicdn.com/t/font_2355444_eortiv1scql.eot?t=1611887868038#iefix")
      format("embedded-opentype"),
    /* IE6-IE8 */
      url("data:application/x-font-woff2;charset=utf-8;base64,d09GMgABAAAAAAKMAAsAAAAABjwAAAJAAAEAAAAAAAAAAAAAAAAAAAAAAAAAAAAAHEIGVgCCcApEWgE2AiQDCAsGAAQgBYRtBzQbhAXILrBt2JMitcAajXCV9CeMB2GIh/9f+98+d+58tSSiUTR/RzVRwqvgjdB1dTwFsmfybD/3ph/IqJz/LL8iVH9AqpDXcnppRufnxFgpPL8Jt0SoZE5Xpf0sygE04Jr6NaCB5AHNrZOikiMBBzYdaFTQyDaSkW8Yu8AlHCfQZFCbdbDcH0NDZo0LxKPQt6GR88kySzYIdTVLs3il1JAepwG8DL8f/2AYDZKyYJUdP1x4MP7JTitq1a77BD8BrS5RYB7IxHlt7FBZMHZZU6xiFOyrOPipqnyr2KtJsL/OKmwB/TAe/OSuECCBHPe2o3fUjaS2uOY/P/1Sm75Pj7XPT2Yf/uxDx9LoUlxZSiv6qY4P7ABU39PP8i5YCD72+s2t9o3/mjP4URNP9T3r5wANO7AHP0LSsyXrMsuSsiqpdSTto8YmNGlCBbu6/I3V9541FRr0nttRbyBFocE4mVnzKDVbR50G22gyZ7W6WTdRFrkRsx4AQod3JG2+odDhg8ysX5T6/KNOR5TR5GJ0b9lsMsLWvpCt5KFzj6HLmXFs2oqKD+RfJ7ZkZSHnlKQIgzhYXC4mV5SRzDGjuPGHqgaNcIpLcBolCWMuHJGr3UA1H/WWHta9qetyCi37BLEp4kGOeyjkYhnjd1et0ucPiO9awiYtFTXhU0QUwv7RQFe/B7lSZ70q7uWVwg3fkFIGMgRLoSUYRBIJhvL6QRHiUl3BiEhupGd3Mn3V3fW16QcUsRosQwp7XqHpjgjfdhIyCgAAAA==")
      format("woff2"),
    url("//at.alicdn.com/t/font_2355444_eortiv1scql.woff?t=1611887868038")
      format("woff"),
    url("//at.alicdn.com/t/font_2355444_eortiv1scql.ttf?t=1611887868038")
      format("truetype"),
    /* chrome, firefox, opera, Safari, Android, iOS 4.2+ */
      url("//at.alicdn.com/t/font_2355444_eortiv1scql.svg?t=1611887868038#iconfont")
      format("svg"); /* iOS 4.1- */
}

.icon-arrow-left:before {
  content: "\e645";
  font-size: 35px;
}
.iconfont {
  font-family: "iconfont" !important;
  font-style: normal;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
.top-1 {
  top: 65px;
}
.top-2 {
  top: 118px;
}
.returnBtn-public {
  width: 50px;
  height: 50px;
  position: fixed;
  left: 30px;
  z-index: 1000;
  >image{
    width: 100%;
    height: 100%;
  }
}
.fixed {
  position: fixed;
}
.titleBar {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100vw;
  color: #fff;
  font-size: 34px;
  background: #ffb300;
  display: flex;
}
.height-1 {
  height: 142px;
  .text {
    margin-top: 30px;
  }
}
.height-2 {
  height: 184px;
  .text {
    margin-top: 84px;
  }
}
</style>