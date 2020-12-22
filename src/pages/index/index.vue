<template>
  <view class="container">
    <view class="avatar">
      <AtAvatar circle :image='avatarUrl'></AtAvatar>
    </view>
    <view class="time">
      <text class="hour">{{ hour }}</text>
      <text class="date">{{ date }}</text>
    </view>
    <view class="poetry">
      <text>从不期待</text>
      <text>很少反抗</text>
      <text>有时落泪</text>
      <text>总是沉默</text>
    </view>
    <view class="begin">
      <text @tap="begin">Let's Begin ></text>
    </view>
  </view>
</template>

<script>
import './index.scss'
import { AtAvatar } from 'taro-ui-vue'

export default {
  components: {
    AtAvatar
  },
  data () {
    return {
      avatarUrl: 'http://5b0988e595225.cdn.sohucs.com/images/20201222/eb0b630f4300411fbcbaccf8460dc8b3.jpeg'
    }
  },
  computed: {
    hour() {
      let date = new Date();
      return date.getHours() + ':' + date.getMinutes();
    },
    date() {
      const days = ["周日", "周一", "周二", "周三", "周四", "周五", "周六"];
      let date = new Date();
      return date.getMonth() + 1 + '月' + date.getDate() + '日' + ' ' + days[date.getDay()];
    }
  },
  methods: {
    begin() {

    },
    authAndGetAvatar() {
      let that = this;
      wx.authorize({
        scope: 'scope.userInfo',
        success () {
          wx.getUserInfo({
            success(res) {
              that.avatarUrl = res.userInfo.avatarUrl;
            }
          })
        }
      })
    }
  },
  mounted() {
    this.authAndGetAvatar();
  }
}
</script>
