<template>
  <div id="app">
    <!-- 动态控制显示渲染视图 -->
    <router-view v-if="isShow" />
  </div>
</template>

<script>
import SSO from '@/sso'
export default {
  data () {
    return {
      // 默认隐藏渲染
      isShow: false
    }
  },
  created () {
    SSO.check((query) => {
      // 输出
      console.log('SSO-Check-App.vue', query)
      // 获取 token 值
      const token = query.token
      // 存储 token 保证接口使用
      // Pub.ACCESS_TOKEN(token || '')
      // token 没值说明没有单点登录记录
      if (!token) {
        // 清空本地用户信息
        // UserInfo.clear()
        // 进入登录或者指定未登录页面
        this.$router.push('/')
      }
      // 显示渲染
      this.isShow = true
    })
  }
}
</script>

<style>
</style>
