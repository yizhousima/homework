<template>
  <div>
      <header class="nav-header">
        <div class="logo-wrap">
            <div class="logo-item">
                <img src="../../static/logo.png">
            </div>
        </div>
        <div class="search-wrap" @click="toSearchPage">
            <div class="search-item">
                <i class="icon iconfont icon-sousuo ico-search"></i>
                搜索商品名称
            </div>
        </div>
        <div class="user-wrap">
            <div class="user-item">
                <div @click="open('/user')"><i class="icon iconfont icon icon-wo ico-user"></i></div>
            </div>
        </div>
    </header>

    <section class="content-wrap">
        <!-- 轮播图 -->
        <div class="banner-wrap">
            <mt-swipe :auto="4000">
                <mt-swipe-item><router-link to="/goodsdetail?id=0003"><img src="/static/lun1.png" alt="one"></router-link></mt-swipe-item>
                <mt-swipe-item><router-link to="/goodsdetail?id=0002"><img src="/static/lun2.png" alt="two"></router-link></mt-swipe-item>
            </mt-swipe>
        </div>
        <!-- 内容区导航栏 -->
        <ul class="nav-list">
            <li class="list-item">
                <a href="">
                    <img src="/static/nuotai01.jpg" alt="">
                </a>
            </li>
            <li class="list-item">
                <a href="">
                    <img src="/static/nuotai02.jpg" alt="">
                </a>
            </li>
            <li class="list-item">
                <a href="">
                    <img src="/static/nuotai03.jpg" alt="">
                </a>
            </li>
            <li class="list-item">
                <a href="">
                    <img src="/static/nuotai04.jpg" alt="">
                </a>
            </li>
            <li class="list-item">
                <a href="">
                    <img src="/static/nuotai05.jpg" alt="">
                </a>
            </li>
        </ul>
        <!-- 商品列表区 -->
        <div class="goods-wrap">
            <!-- 大图区 -->
            <ul class="big-item-list">
                <li class="big-item"><router-link to="/goodsdetail?id=0012"><img src="/static/meirijingxuan.jpg" alt=""></router-link></li>
                <li class="big-item"><router-link to="/goodsdetail?id=0013"><img src="/static/chaozhituijian.jpg" alt=""></router-link></li>
            </ul>
            <!-- 小图区 -->
            <ul class="normal-item-list clearfix">
                <li class="normal-item" v-for="item in goodsList" @click="viewGoods(item.goodsId)">
                    <div class="img">
                        <img :src="'/static/' + item.goodsImg" alt="">
                    </div>
                    <div class="info">
                        <div class="name">{{item.goodsName}}</div>
                        <div class="brief">{{item.goodsBrief}}</div>
                        <div class="price">
                            ￥{{item.goodsPrice}}
                        </div>
                    </div>
                </li>
            </ul>
        </div>
    </section>

    <!-- <nav-footer></nav-footer> -->
  </div>
</template>

<script>
import '@/assets/css/reset.css'
import '@/assets/css/homepage.css'
// import NavFooter from '@/components/NavFooter'
import { Swipe, SwipeItem } from 'mint-ui'
import axios from 'axios'
export default {
  data(){
      return {
          goodsList: []
      }
  },
  components: {
      
  },
  mounted:function(){
      this.init();
  },
  methods: {
      init(){
          // 如果想访问json文件，应把文件放在static文件夹中，这个文件夹是vue-cli内置服务器向外暴露的静态文件夹
          axios.get('/static/mock/Home.json').then(result=>{
              var goodsData = result.data;
              this.goodsList = goodsData.goodsList;
          });
      },
      toSearchPage(){
          this.$router.push({
              path: 'search'
          });
      },
      viewGoods(goodsId){
          this.$router.push({
              path: 'goodsdetail',
              query: {id: goodsId}
          });
      },
      open(path){
          this.$router.push({
              path: path
          });
      }
  }
}
</script>

<style>
    .banner-wrap{
        height: 8rem;
    }
    .banner-wrap img{
        width: 100%;
        height: 8rem;
    }
</style>

