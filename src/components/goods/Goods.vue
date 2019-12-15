<template>
  <div class="goods">
    <div class="menu-wrapper" ref="menuScroll">
      <ul>
        <!-- 专场 -->
        <li 
          class="menu-item" 
          @click="selectMenu(0)">
          <p class="text">
            <img class="icon" :src="container.tag_icon" v-if="container.tag_icon">
            {{ container.tag_name }}
          </p>
        </li>

        <li 
          class="menu-item" 
          v-for="(item, index) in goods" :key="index"
          @click="selectMenu(index+1)">
          <p class="text">
            <img class="icon" :src="item.icon" v-if="item.icon">
            {{ item.name }}
          </p>
        </li>
      </ul>
    </div>
    <div class="foods-wrapper" ref="foodsScroll">
      <ul>
        <!-- 专场 -->
         <li class="container-list food-list-hook">
           <div v-for="(item,index) in container.operation_source_list" :key="index">
            <img :src="item.pic_url">
          </div>
         </li>

         <!-- 具体分类 -->
         <li v-for="(item,index) in goods" :key="index" class="food-list food-list-hook">
          <h3 class="title">{{item.name}}</h3>

          <!-- 具体的商品列表 -->
          <ul>
            <li 
              v-for="(food,index) in item.spus" 
              :key="index" 
              class="food-item">
              <div class="icon" :style="head_bg(food.picture)"></div>
              <div class="content">
                <h3 class="name">{{food.name}}</h3>
                <p class="desc" v-if="food.description">{{food.description}}</p>
                <div class="extra">
                  <span class="saled">{{food.month_saled_content}}</span>
                  <span class="praise">{{food.praise_content}}</span>
                </div>
                <img class="product" :src="food.product_label_picture" alt="">
                <p class="price">
                  <span class="text">￥{{food.min_price}}</span>
                  <span class="unit">/{{food.unit}}</span>
                </p>
              </div>
            </li>
          </ul>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import BScroll from 'better-scroll'
export default {
  name: 'Goods',
  data () {
    return {
      container: {},
      goods: [],
      poiInfo: {}
    }
  },
  methods: {
    initScroll () {
      new BScroll(this.$refs.menuScroll)
      new BScroll(this.$refs.foodsScroll)
    },
    getAllData () {
      axios.get('./api/goods.json')
        .then(res => {
          if (res && res.data.code === 0) {
            const data = res.data.data
            this.container = data.container_operation_source
            this.goods = data.food_spu_tags
            this.poiInfo = data.poi_info
            console.log(data)
            this.initScroll()

          }
      })
    },
    head_bg (pic) {
      return "backgroundImage: url(" + pic + ")"
    }
  },
  created () {
    this.getAllData()
  }
}
</script>

<style>
.goods{
  display: flex;
  position: absolute;
  top: 190px;
  left: 0;
  bottom: 51px;
  overflow: hidden;
  width: 100%;
}
.menu-wrapper{
  flex: 0 0 85px;
  background: #f4f4f4;
}
.foods-wrapper{
  flex: 1;
}
/* Menu item */ 
.goods .menu-wrapper .menu-item{
	padding: 16px 23px 15px 10px;
	border-bottom: 1px solid #E4E4E4;
  position: relative;
}
.goods .menu-wrapper .menu-item .text{
	font-size: 13px;
	color: #333333;
	line-height: 17px;
	vertical-align: middle;
	-webkit-line-clamp: 2;
	display: -webkit-box;
	-webkit-box-orient: vertical;
	overflow: hidden;
}

.goods .menu-wrapper .menu-item .text .icon{
	width: 15px;
	height: 15px;
	vertical-align: middle;
}

.goods .foods-wrapper .container-list{
	padding: 11px 11px 0 11px;
	border-bottom: 1px solid #E4E4E4;
}

.goods .foods-wrapper .container-list img{
	width: 100%;
	margin-bottom: 11px;
	border-radius: 5px;
}
/* 具体分类商品布局 */ 
.goods .foods-wrapper .food-list{
	padding: 11px;
}

.goods .foods-wrapper .food-list .title{
	height: 13px;
	font-size: 13px;
	background: url(./img/btn_yellow_highlighted@2x.png) no-repeat left center;
	background-size: 2px 10px;
	padding-left: 7px;
	margin-bottom: 12px;
}

.goods .foods-wrapper .food-list .food-item{
	display: flex;
	margin-bottom: 25px;
  position: relative;
}

.goods .foods-wrapper .food-list .food-item  .icon{
	flex: 0 0 63px;
	background-position: center;
	background-size: 120% 100%;background-repeat: no-repeat;
	margin-right: 11px;
	height: 75px;
}
.goods .foods-wrapper .food-list .food-item .content{
	flex: 1;
}

/* 具体内容样式 */ 
.goods .foods-wrapper .food-list .food-item .content .name{
	font-size: 16px;
	line-height: 21px;
	color: #333333;
	margin-bottom: 10px;
	padding-right: 27px;
}

.goods .foods-wrapper .food-list .food-item .content .desc{
	font-size: 10px;
	line-height: 19px;
	color: #bfbfbf;
	margin-bottom: 8px;
	
	/* 超出部分显示省略号*/
	-webkit-line-clamp: 1;
	display: -webkit-box;
	-webkit-box-orient: vertical;
	overflow: hidden;
}

.goods .foods-wrapper .food-list .food-item .content .extra{
	font-size: 10px;
	color: #BFBFBF;
	margin-bottom: 7px;
}
.goods .foods-wrapper .food-list .food-item .content .extra .saled{
	margin-right: 14px;
}
.goods .foods-wrapper .food-list .food-item .content .product{
	height: 15px;
	margin-bottom: 6px;
}
.goods .foods-wrapper .food-list .food-item .content .price{
	font-size: 0;
}
.goods .foods-wrapper .food-list .food-item .content .price .text{
	font-size: 14px;
	color: #fb4e44;
}
.goods .foods-wrapper .food-list .food-item .content .price .unit{
	font-size: 12px;
	color: #BFBFBF;
}
</style>