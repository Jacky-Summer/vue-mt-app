<template>
  <div id="app">
    <!-- 头部信息 -->
    <app-header :poiInfo="poiInfo"></app-header>
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
import axios from 'axios'
export default {
  name: 'App',
  data () {
    return {
      poiInfo: {}
    }
  },
  components: {
    'app-header': Header,
    'app-nav': Nav
  },
  methods: {
    getGoodsData () {
      axios.get('./api/goods.json')
        .then(res => {
          if(res && res.data.code === 0) {
            const data = res.data.data;
            this.poiInfo = data.poi_info
          }
        })
    }
  },
  created () {
    this.getGoodsData()
  }
}
</script>

<style>

</style>
