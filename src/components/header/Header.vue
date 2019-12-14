<template>
  <div class="header">
    <div class="top-wrapper">
      <div class="back-wrapper">
        <span class="icon-arrow_lift"></span>
      </div>
      <div class="search-wrapper">
        <span class="search-icon"></span>
        <input type="text" class="search-bar" placeholder="搜索店内商品">
      </div>
      <div class="more-wrapper">
        <a class="spelling-bt" href="#">拼单</a>
        <div class="more-bt">
          <i class="s-radius"></i>
          <i class="s-radius"></i>
          <i class="s-radius"></i>
        </div>
      </div>
    </div>

    <div class="content-wrapper">
      <div class="icon" :style="head_bg"></div>
      <div class="name">
        <h3>{{ poiInfo.name }}</h3>
      </div>
      <div class="collect">
        <img src="./img/star.png">
        <span>收藏</span>
      </div>
    </div>

    <!-- 背景内容 开始 -->
    <div class="bg-wrapper" :style="head_pic_url"></div>
    <!-- 背景内容 结束 -->

    <!-- 公告内容 开始 -->
    <div class="bulletin-wrapper">
			<img class="icon" v-if="poiInfo.discounts2" :src="poiInfo.discounts2[0].icon_url"/>

			<span class="text" v-if="poiInfo.discounts2">{{ poiInfo.discounts2[0].info }}</span>
			<div class="detail" v-if="poiInfo.discounts2">
				{{ poiInfo.discounts2.length }}个活动
				<span class="icon-keyboard_arrow_right"></span>
			</div>
		</div> 
    <!-- 公告内容 结束 -->

  </div>
</template>

<script>
export default {
  name: 'Header',
  data () {
    return {

    }
  },
  props: {
    poiInfo: {
      type:Object,
      default:{}
    }
  },
  computed: {
    head_pic_url () {
      return "backgroundImage: url(" + this.poiInfo.head_pic_url + ")"
    },
    head_bg(){
      return "background-image: url(" + this.poiInfo.pic_url + ");"
    },
  }
}
</script>

<style scoped>
@import url(../../common/css/icon.css);
.header{
  height: 130px;
  padding-top: 20px;
}
.header .top-wrapper {
	position: relative;
}
	
.header .top-wrapper .back-wrapper {
  width: 50px;
  height: 31px;
  position: absolute;
  left: 0;
  top: 0;
  text-align: center;
  line-height: 31px;
}
.header .top-wrapper .back-wrapper span {
  display: inline-block;
  color: white;
}

.header .search-wrapper{
  width: 100%;
  height: 31px;
  padding: 0 104px 0 50px;
  box-sizing: border-box;
  position: relative;
}
.header .search-wrapper .search-icon{
  background: url(./img/search.png) no-repeat 11px center;
  position: absolute;
  width: 28px;
  height: 31px;
  background-size: 13px 13px;
}
.header .search-wrapper .search-bar{
  width: 100%;
  background-color: #cdcdcc;
  border: 0;
  height: 31px;
  border-radius: 25px;
  padding-left: 28px;
  box-sizing: border-box;
  outline: none;
}
.header .more-wrapper{
  width: 65px;
  height: 24px;
  position: absolute;
  right: 0;
  top: 0;
  padding: 7px 15px 0 24px;
}
.header .more-wrapper .spelling-bt{
  width: 30px;
  height: 17px;
  color: white;
  line-height: 17px;
  border: 1px solid white;
  text-align: center;
  float: left;
  text-decoration: none;
  font-size: 10px;
}
.header .top-wrapper .more-wrapper .more-bt {
  float: right;
  width: 20px;
  height: 24px;
  margin-left: 13px;
  margin-top: 6px;
}
.header .top-wrapper .more-wrapper .more-bt .s-radius {
  width: 3px;
  height: 3px;
  border-radius: 50%;
  border: 1px solid white;
  display: block;
  float: left;
  margin-right: 1px;
}
/* 背景图片样式 */ 
.header .bg-wrapper {
  width: 100%;
  height: 150px;
  position: absolute;
  left: 0;
  top: 0;
  z-index: -1;
  background-size: 100% 135%;
  background-position: center -12px;
}

/* 主题内容 样式 */ 
.header .content-wrapper {
  padding: 17px 5px 6px;
  height: 50px;
}

.header .content-wrapper .icon {
  width: 50px;
  height: 100%;
  background-size: 135% 100%;
  background-position: center;
  border-radius: 5px;
  float: left;
}
.header .content-wrapper .name {
  float: left;
  padding-left: 12px;
}

.header .content-wrapper .name h3 {
  font-size: 16px;
  font-weight: bold;
  color: white;
}
.header .content-wrapper .collect {
  width: 25px;
  height: 37px;
  float: right;
  text-align: center;
  padding-top: 6px;
}
.header .content-wrapper .collect img {
  width: 20px;
  height: 20px;
}
.header .content-wrapper .collect span {
  color: white;
  font-size: 11px;
}
/* 公告内容样式 */
.header .bulletin-wrapper {
  height: 16px;
  padding: 0 5px;
}

.header .bulletin-wrapper .icon {
  width: 16px;
  height: 16px;
  float: left;
  margin-right: 3px;
}

.header .bulletin-wrapper .text {
  font-size: 11px;
  color: white;
  float: left;
  line-height: 16px;
}

.header .bulletin-wrapper .detail {
  color: white;
  float: right;
  font-size: 11px;
  line-height: 16px;
}

.header .bulletin-wrapper .detail span {
  font-size: 16px;
  line-height: 16px;
  float: right;
}
</style>