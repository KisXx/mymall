<template>
  <div id="home">
    <nav-bar class="home-nav">
      <div slot="center">购物街</div>
    </nav-bar>
    <scroll class="content" 
            ref="scroll" 
            :probe-type="3" 
            :pull-up-load="true" 
            @scroll="contentScroll"
            @pullingUp="loadMore">
      <home-swiper :banners="banners"></home-swiper>
      <home-recommend-view :recommends="recommends"></home-recommend-view>
      <feature-view/>
      <tab-control class="tab-control" :titles="['流行','新款','精选']" @TabControlClick="TabControlClick"/>
      <goods-list :goods="showGoods"/>
    </scroll>
    <back-top @click.native="backClick" v-show="isShowBackTop"/>
  </div>
</template>

<script>
  import NavBar from 'components/common/navbar/NavBar'
  import TabControl from 'components/content/tabControl/TabControl'
  import GoodsList from 'components/content/goods/GoodsList'
  import Scroll from 'components/common/scroll/Scroll'
  import BackTop from 'components/content/backTop/BackTop'

  import HomeSwiper from './childComps/HomeSwiper'
  import HomeRecommendView from './childComps/HomeRecommendView'
  import FeatureView from './childComps/FeatureView'

  import {getHomeMultidata, getHomeGoods} from 'network/home'

  export default {
    name:'home',
    components:{
      NavBar,
      HomeSwiper,
      HomeRecommendView,
      FeatureView,
      TabControl,
      GoodsList,
      Scroll,
      BackTop
    },
    data(){
      return{
        banners: [],
        recommends: [],
        goods: {
          'pop': {page: 0, list: []},
          'new': {page: 0, list: []},
          'sell': {page: 0, list: []}
        },
        currentGoods: 'pop',
        isShowBackTop: false
      }
    },
    computed: {
      showGoods(){
        return this.goods[this.currentGoods].list
      }
    },
    created(){
      //请求多个数据
      this.getHomeMultidata();

      //请求商品数据
      this.getHomeGoods('pop');
      this.getHomeGoods('new');
      this.getHomeGoods('sell');
    },
    methods: {
      getHomeMultidata(){
        getHomeMultidata().then(res =>{
          this.banners = res.data.banner.list;
          this.recommends = res.data.recommend.list;
        })
      },
      getHomeGoods(type){
        const page = this.goods[type].page + 1;
        getHomeGoods(type, page).then(res => {
          this.goods[type].list.push(...res.data.list);
          this.goods[type].page += 1;

          this.$refs.scroll.finishPullUp()
        })
      },

      TabControlClick(index){
        switch (index) {
          case 0:
            this.currentGoods = 'pop';
            break;
          case 1:
            this.currentGoods = 'new';
            break;
          case 2:
            this.currentGoods = 'sell';
            break;
        }
      },

      backClick(){
        this.$refs.scroll.scrollTo(0, 0)
      },

      contentScroll(position){
        this.isShowBackTop =  -position.y > 1000
      },

      loadMore(){
        this.getHomeGoods(this.currentGoods);
      }
    }
  }
</script>

<style scoped>
  #home{
    height: 100vh;
    position: relative;
  }

  .home-nav{
    background-color: var(--color-tint);
    color: #fff;

    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    z-index: 9;
  }

  .tab-control{
    top: 44px;
    z-index: 9;
  }

  .content{
    height: calc(100% - 93px);
    overflow: hidden;
    margin-top: 44px;
  }
</style>