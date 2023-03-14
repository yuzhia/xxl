<template>
  <view class="container" ref="divRef">
    <view v-show="flag" class="welcome">
      <img class="title-img" src="@/assets/images/text.png" />
      <button class="change-btn rounded" @click="handleStart">
    
        开始游戏
      </button>
    </view>
    <view class="score text-red!">{{ score }}分</view>
    <view class="stage">
      <view
        v-for="item in data"
        :style="{
          left: `${item.positionLeft}px`,
          top: `${item.positionTop}px`
        }"
        :key="item.key"
        :class="[
          'square',
          `type${item.type}`,
          `scale${item.scale}`,
          { active: item.active }
        ]"
        @click="handleClick(item)"
      ></view>
    </view>
    <view>
      <button class="change-btn" @click="handleOver">
        结束游戏
      </button>
    </view>
  </view>
</template>
<script lang="ts" setup>
import Stage from '@/utils/stage'
const flag = ref(true)
const divRef = ref(null)

const width = ref()

uni.getSystemInfo({
  success: function (res) {
    width.value = res.screenWidth
  }
})

// uni.getUserInfo({
//   provider: 'weixin',
//   success: (res) => {
//     console.log('getUserInfo', res)
//   }
// })
// let width: number = document.documentElement.clientWidth
console.log(width.value)
const games = reactive(new Stage(7, 7, (width.value - 20) / 7))
const { data, score } = toRefs(games)

// 开始游戏
const handleStart = () => {
  flag.value = false
  games.gameLoop(true)
}
// 选择方块
const handleClick = (item: any) => {
  games.click(item)
}
// 结束游戏
const handleOver = () => {
  console.log('当前成绩0')
  flag.value = true
  // ElMessageBox.alert(`当前成绩：${score.value}分`, "雪糕消消大作战", {
  //   confirmButtonText: "确定",
  //   callback: (action: Action) => {
  //     flag.value = true
  //   },
  // })
}
</script>
<style lang="scss" scoped>
@function px2vw($px) {
  @return calc($px / 375 * 100vw);
}
.container {
  display: flex;
  align-items: center;
  justify-content: center;
  width: px2vw(375);
  height: 100vh;
  background-color: #ccc;
  // background-image: url("@/assets/images/bg.jpg");
  background-size: 100% 100%;
  .stage {
    position: relative;
    width: calc(100vw - 20px);
    height: calc(100vw - 20px);
    background-color: rgba(116, 183, 187, 0.7);
    border: 1px solid #fff;
    .square {
      position: absolute;
      width: px2vw(calc(355 / 7));
      height: px2vw(calc(355 / 7));
      border: 1px solid #fff;
      box-sizing: border-box;
      transition: 0.5s;
      background-repeat: no-repeat;
      background-size: 85% 85%;
      background-position: center;
    }
    .type0 {
      background-image: url('@/assets/images/0.png');
    }
    .type1 {
      background-image: url('@/assets/images/1.png');
    }
    .type2 {
      background-image: url('@/assets/images/2.png');
    }
    .type3 {
      background-image: url('@/assets/images/3.png');
    }
    .type4 {
      background-image: url('@/assets/images/4.png');
    }
    .type5 {
      background-image: url('@/assets/images/5.png');
    }
    .type6 {
      background-image: url('@/assets/images/6.png');
    }
    .active {
      background-color: #f0f;
    }
    .scale0 {
      transform: scale(0);
      z-index: 0;
    }
    .scale1 {
      transform: scale(1);
      z-index: 1;
    }
  }
  .welcome {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    // background-image: url('@/assets/images/bg.jpg');
    background-size: 100% 100%;
    z-index: 2;
    overflow: hidden;
    .title-img {
      margin-top: px2vw(200);
      width: 100%;
      transform: rotate(-10deg);
    }
  }
  .score {
    position: absolute;
    top: px2vw(30);
    font-weight: bold;
    font-size: px2vw(28);
    color: #fff;
  }
  .change-btn {
    position: absolute;
    bottom: px2vw(50);
    left: 50%;
    transform: translateX(-50%);
  }
}
</style>
