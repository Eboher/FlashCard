<template>
  <view class="container">
    <view class="content" @tap="changeSide">
      <wemark :md="cardData" link :highlight="true" type="wemark"></wemark>
    </view>
    <view class="btn-area">
      <AtButton type='primary' :onClick="pre">  上一个 </AtButton>
      <AtButton type='primary' :onClick="next"> 下一个 </AtButton>
    </view>
  </view>
</template>

<script>
import './card.scss'
import Cards from '@/static/data/cards.ts'
import { AtButton } from 'taro-ui-vue'

export default {
  components: {
    AtButton
  },
  mixins: [Cards],
  data() {
    return {
      index: 0,
      side: "front"
    }
  },
  computed: {
    cardData() {
      return this.card[this.index][this.side];
    }
  },
  watch: {
    index() {
      this.saveIndex();
    }
  },
  methods: {
    changeSide() {
      const anotherSide = {
        front: "back",
        back: "front"
      };
      this.side = anotherSide[this.side];
    },
    changeToFront() {
      this.side = "front";
    },
    pre () {
      this.changeToFront();
      if (this.index > 0) {
        this.index --;
      } else {
        this.index = this.card.length - 1;
      }
    },
    next() {
      this.changeToFront();
      if (this.index < this.card.length - 1) {
        this.index++;
      }else {
        this.index = 0;
      }
    },
    saveIndex() {
      wx.setStorage({
        key:"index",
        data:this.index
      })
    },
    getIndex() {
      return wx.getStorageSync('index');
    }
  },
  mounted() {
    this.changeToFront();
    this.index = this.getIndex() || 0;
  }
}
</script>
