<template>
  <view class="flex flex-col gap-10 mt-20 items-center px-10">
    <view class="text-center">
      <view>
        <image
          class="w-150 h-150 border-sky border-solid rounded-full"
          :src="avatarUrl"
          mode="aspectFill"
        ></image>
      </view>
      <text v-if="!avatarUrl">请登录</text>
    </view>
    <button
      class="w-full"
      type="primary"
      open-type="chooseAvatar"
      @chooseavatar="onChooseAvatar"
    >
      登录
    </button>
  </view>
</template>

<script lang="ts" setup>
const avatarUrl = ref('')

const onChooseAvatar = (e: any) => {
  console.log(e)
  avatarUrl.value = e.target.avatarUrl
}
</script>
