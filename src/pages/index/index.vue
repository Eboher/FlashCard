<template>
  <view class="container">
    <view class="avatar">
      <AtAvatar circle :openData="{ type: 'userAvatarUrl'}"></AtAvatar>
    </view>
    <view class="time">
      <text class="hour">{{ hour }}</text>
      <text class="date">{{ date }}</text>
    </view>
    <view class="begin">
      <text @tap="begin">开始</text>
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

    }
  },
  computed: {
    hour() {
      let date = new Date();
      return date.getHours() + ':' + (date.getMinutes() < 10 ? '0' : '') + date.getMinutes();
    },
    date() {
      const days = ["周日", "周一", "周二", "周三", "周四", "周五", "周六"];
      let date = new Date();
      return date.getMonth() + 1 + '月' + date.getDate() + '日' + ' ' + days[date.getDay()];
    }
  },
  methods: {
    begin() {
      wx.navigateTo({
          url: '/pages/card/card'
      })
    }
  }
}
</script>
