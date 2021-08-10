<template>
  <div id="app">
    <!-- 动态控制显示渲染视图 -->
    <router-view v-if="isShow" />
  </div>
</template>

<script>
import SSO from '@/sso'
// import { userInfo, reloadToken } from '@/api/request'
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
      if (token) {
        // 获取用户信息数据
        // this.userInfo()

        // 调用刷新 token 接口（看服务器是否要求需要刷新 token，不需要用上面的直接调用即可）
        // reloadToken().then(() => {
        //   // 获取用户信息
        //   this.userInfo()
        // }).catch(() => {
        //   // 获取用户信息
        //   this.userInfo()
        // })

        // 显示渲染（可以放到获取用户信息回调中，成功或失败都得打开显示）
        this.isShow = true
      } else {
        // 清空本地用户信息
        // UserInfo.clear()

        // 进入登录或者指定未登录页面
        this.$router.push('/')

        // 进入登录或者指定未登录页面(如果有原生首页 与 Vue结合使用的，需要判断一下是否在登录页，在登录页则不需要进入首页)
        // if (!window.location.href.includes('/login')) {
        //   // 非登录页获取失败都进入首页
        //   this.$router.push('/')
        // }

        // 显示渲染（延迟渲染是为了防止在当前页面刷新需要跳转到其他页面出现的闪动，保证效果流畅，如果还是出现页面闪动，添加时间即可）
        setTimeout(() => {
          this.isShow = true
        }, 80)
      }
    })
  },
  methods: {
    // 获取用户信息（案例）
    userInfo () {
      // 获取用户数据
      // userInfo().then(res => {
      //   const { code, data } = res
      //   if (code === 0) {
      //     // 更新用户信息
      //     this.$store.commit('SET_USER_INO', data)
      //     // 进入登录成功页面
      //     this.$router.push('/home')
      //   } else {
      //     // 清空本地用户信息
      //     UserInfo.clear()
      //     // 进入登录或者指定未登录页面
      //     this.$router.push('/')
      //   }
      //   // 显示渲染（延迟渲染是为了防止在当前页面刷新需要跳转到其他页面出现的闪动，保证效果流畅，如果还是出现页面闪动，添加时间即可）
      //   setTimeout(() => {
      //     this.isShow = true
      //   }, 80)
      // }).catch((err) => {
      //   // 清空本地用户信息
      //   UserInfo.clear()
      //   // 进入登录或者指定未登录页面
      //   this.$router.push('/')
      //   // 显示渲染（延迟渲染是为了防止在当前页面刷新需要跳转到其他页面出现的闪动，保证效果流畅，如果还是出现页面闪动，添加时间即可）
      //   setTimeout(() => {
      //     this.isShow = true
      //   }, 80)
      // })
    }
  }
}
</script>

<style>
</style>
