<template>
  <view class="index">
    <text>{{ msg }}</text>

    <button
      type="primary"
      open-type="getAuthorize"
      scope="userInfo"
      :onGetUserInfo="onGetUserInfo"
      @get-user-info="onGetUserInfo"
      @tap="onTap"
      @error="onError"
    >
      前往授权
    </button>
  </view>
</template>

<script>
import { ref } from 'vue'
import './index.scss'

export default {
  setup () {
    const msg = ref('Hello world')

    function onGetUserInfo() {
      console.log('onGetUserInfo')
    }

    function onTap() {
      console.log('tap')
    }

    function onError(err) {
      console.log('error', err)
    }


    return {
      msg,
      onGetUserInfo,
      onTap,
      onError,
    }
  }
}
</script>
