<template>
  <div class="content-view">
    <div>打开控制台，查看输出信息</div>
    <button @click="touchLogin">登录</button>
    <button @click="touchLogout">退出</button>
    <button @click="touchCheck">检查（示例代码在 App.vue 中）</button>
  </div>
</template>

<script>
import SSO from '@/sso'
export default {
  methods: {
    // 登录
    touchLogin () {
      // 登录服务器获得到的 token
      const token = 'SSO-TEST-TOKEN'
      // 进行单点登录
      SSO.login(token, (query) => {
        // 输出返回信息 { sso: 1, storage: 1, type: 'logout', token: 'xxx' }
        console.log('SSO-Login', query)
        // 进行登录成功处理

        // -------------- 案例 --------------
        // 1、通过 token 获取用户信息
        // 2、进入登录成功页面
      })
    },
    // 退出
    touchLogout () {
      // 退出单点登录
      SSO.logout((query) => {
        // 输出返回信息 { sso: 1, storage: 1, type: 'logout', token: 'xxx' }
        console.log('SSO-Logout', query)
        // 进行退出成功处理

        // -------------- 案例 --------------
        // 1、清空本地用户信息
        // 2、进入登录或者指定未登录页面
      })
    },
    // 检查
    touchCheck () {
      // 检查当前浏览器是否存在单点登录 token
      SSO.check((query) => {
        // 输出返回信息 { sso: 1, storage: 1, type: 'logout', token: 'xxx' }
        console.log('SSO-Check', query)
        // 进行检查成功处理

        // -------------- 案例 --------------
        // 获取 token 值
        const token = query.token
        // 1、存储 token 保证接口使用，或保证 Vue 使用
        // localStorage.setItem('token', token || '')
        // 2、token 没值说明没有单点登录记录
        if (token) {
          // 获取到单点登录 token 进行获取用户信息操作
          // axios.get(url,params).then(res => {
          //   console.log(res)
          //   // 1、获取成功存储用户数据进入指定登录成功页面
          //   // 2、加载失败退出登录
          // }).catch(err => {
          //   console.error(err)
          //   // 1、加载失败退出登录
          //   // 清空本地用户信息
          //   UserInfo.clear()
          //   // 进入登录或者指定未登录页面
          //   this.$router.push('/')
          // })
        } else {
          // 1、没有 token 退出登录
          // 清空本地用户信息
          // UserInfo.clear()
          // 进入登录或者指定未登录页面
          // this.$router.push('/')
        }
      })
    }
  }
}
</script>

<style scoped>
.content-view {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.content-view button {
  margin-top: 15px;
}
</style>
