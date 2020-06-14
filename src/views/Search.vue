<template>
    <div>
        <header class="search-header">
            <div class="header-back">
                <a href="javascript:;" class="header-back-item" @click="back">
                    <i class="icon iconfont icon-fanhui1 ico-back"></i>
                </a>
            </div>
            <div class="input-box">
                <input type="text" class="input-text" v-model="inputText" placeholder="搜索商品名称">
            </div>
            <div class="search-logo-box">
                <div class="search-logo">
                    <i class="icon iconfont icon-sousuo ico-search"></i>
                </div>
            </div>
        </header>
        <div class="hot-search">
            <div class="title">热门搜索</div>
            <div class="img">
                <router-link to="/goodsdetail?id=0012">
                    <img src="https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1592132732035&di=576ab4828e2cc46b90781f02bdd9a1f2&imgtype=0&src=http%3A%2F%2Fpic.rmb.bdstatic.com%2F37f4985b8cbb81eb5d52384437861efe.jpeg" alt="">
                </router-link>
            </div>
        </div>
        
        <div class="search-goods-list">
            <ul class="goods-list">
                <li class="list-item" v-for="item in searchList" @click="viewGoods(item.goodsId)">{{item.goodsName}}</li>
            </ul>
        </div>
    </div>
</template>

<script>
import '@/assets/css/reset.css'
import '@/assets/css/search.css'
import axios from 'axios'
export default {
    data(){
        return {
            goodsList: [],
            inputText: ''
        }
    },
    mounted: function(){
        this.init();
    },
    computed: {
        searchList: function(){
            var searchListArr = [];

            if(this.inputText == ''){
                return searchListArr;
            }

            this.goodsList.forEach(item=>{
                if(item.goodsName.toLowerCase().indexOf(this.inputText.toLowerCase()) != -1){
                    searchListArr.push(item);
                }
            });

            return searchListArr;
        }
    },
    methods: {
        init(){
            axios.get('/static/mock/Categories.json').then(result=>{
                var goodsData = result.data;
                this.goodsList = goodsData.allGoods;
            });
        },
        back(){
            this.$router.push({
                path: '/'
            });
        },
        viewGoods(id){
            this.$router.push({
                path: 'goodsdetail',
                query: {id: id}
            });
        }
    }
}
</script>

