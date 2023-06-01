# 复现仓库: Taro-Vue3-支付宝小程序 &lt;button&gt;特定事件无法触发

## 复现步骤

1. 创建项目

   ```powershell
   PS D:\temp> npx @tarojs/cli@3.6.7 init taro-ali-event-demo
   ? 请输入项目介绍 taro-ali-event-demo
   ? 请选择框架 Vue3
   ? 是否需要使用 TypeScript ？ Yes
   ? 请选择 CSS 预处理器（Sass/Less/Stylus） Sass
   ? 请选择编译工具 Webpack5
   ? 请选择包管理工具 pnpm
   ? 请选择模板源 Github（最新）
   ✔ 拉取远程模板仓库成功！
   ? 请选择模板 默认模板
   
   
   
   PS D:\temp> cd .\taro-ali-event-demo\
   # 解决版本问题报错 Error: Cannot find module 'vue/compiler-sfc'
   PS D:\temp\taro-ali-event-demo> pnpm i vue@latest
   ```

   

2. 修改 `src/pages/index/index.vue` 文件

   ```diff
   @@ -1,6 +1,18 @@
    <template>
      <view class="index">
        <text>{{ msg }}</text>
   +
   +    <button
   +      type="primary"
   +      open-type="getAuthorize"
   +      scope="userInfo"
   +      :onGetUserInfo="onGetUserInfo"
   +      @get-user-info="onGetUserInfo"
   +      @tap="onTap"
   +      @error="onError"
   +    >
   +      前往授权
   +    </button>
      </view>
    </template>
   
   @@ -11,8 +23,25 @@ import './index.scss'
    export default {
      setup () {
        const msg = ref('Hello world')
   +
   +    function onGetUserInfo() {
   +      console.log('onGetUserInfo')
   +    }
   +
   +    function onTap() {
   +      console.log('tap')
   +    }
   +
   +    function onError(err) {
   +      console.log('error', err)
   +    }
   +
   +
        return {
   -      msg
   +      msg,
   +      onGetUserInfo,
   +      onTap,
   +      onError,
        }
      }
    }
   ```


3. build

   ```powershell
   PS D:\temp\taro-ali-event-demo> npm run build:alipay
   ```
4. 现象: 点击 `前往授权` 按钮弹出授权框, 同意后未打印 error 和 onGetUserInfo
