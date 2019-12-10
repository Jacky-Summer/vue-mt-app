<template>
  <div id="app">
    <!-- 头部信息 -->
    <app-header></app-header>
    <!-- 导航 -->
    <div class="nav">
      <app-nav></app-nav>
    </div>
    <!-- 内容 -->
    <div class="content">
      <router-view></router-view>
    </div>

  </div>
</template>

<script>
import Header from '@/components/header/Header'
import Nav from '@/components/nav/Nav'
import Goods from '@/components/goods/Goods'
export default {
  name: 'App',
  components: {
    'app-header': Header,
    'app-nav': Nav
  }
}
</script>

<style>

</style>
