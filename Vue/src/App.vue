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
      // 判断当前是否支持 Storage 使用
      if (!query.storage) {
        // 不允许使用则打开显示
        this.isShow = true
        // 禁止往下走
        return
      }
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
        // 加载失败退出登录
        // this.logout()

        //（Vue 与 原生混合开发时）进入登录或者指定未登录页面(如果有原生首页 与 Vue结合使用的，需要判断一下是否在登录页，在登录页则不需要进入首页)
        // if (!window.location.href.includes('/login')) {
        //   // 非登录页获取失败都进入首页
        //   this.$router.push('/')
        // }
      }
    })
  },
  methods: {
    // 获取用户信息（案例）
    // userInfo () {
    //   // 获取用户数据
    //   userInfo().then(res => {
    //     const { code, data } = res
    //     if (code === 0) {
    //       // 更新用户信息
    //       this.$store.commit('SET_USER_INO', data)
    //       // 如果是登录页，才需要跳转到指定页面（防止用户直接输入全地址访问，或者当前页面刷新被重新定位到其他页面）
    //       if (window.location.href.includes('/login')) {
    //         this.$router.push('/home')
    //       }
    //     } else {
    //       // 加载失败退出登录
    //       this.logout()
    //       // 进入登录失败页面
    //       this.$router.push('/login-error')
    //     }
    //   }).catch(() => {
    //     // 加载失败退出登录
    //     this.logout()
    //     // 进入登录失败页面
    //     this.$router.push('/login-error')
    //   })
    // },
    // // 退出登录
    // logout () {
    //   // 清空本地用户信息
    //   UserInfo.clear()
    //   // 进入登录或者指定未登录页面
    //   this.$router.push('/')
    //   // 显示渲染（延迟渲染是为了防止在当前页面刷新需要跳转到其他页面出现的闪动，保证效果流畅，如果还是出现页面闪动，添加时间即可）
    //   setTimeout(() => {
    //     this.isShow = true
    //   }, 80)
    // }
  }
}
</script>

<style>
</style>
