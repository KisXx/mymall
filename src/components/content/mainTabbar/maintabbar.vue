<template>
  <div>
    <tabbar>
      <tabbarItem path="/home">
      <img src="~assets/img/tabbar/home.svg" slot="item-icon">
      <img src="~assets/img/tabbar/home_active.svg" slot="item-icon-active">
      <div slot="item-text">首页</div>
    </tabbarItem>
    <tabbarItem path="/category">
      <img src="~assets/img/tabbar/category.svg" slot="item-icon">
      <img src="~assets/img/tabbar/category_active.svg" slot="item-icon-active">
      <div slot="item-text">关于</div>
    </tabbarItem>
    <tabbarItem path="/cart">
      <img src="~assets/img/tabbar/shopcart.svg" slot="item-icon">
      <img src="~assets/img/tabbar/shopcart_active.svg" slot="item-icon-active">
      <div slot="item-text">购物车</div>
    </tabbarItem>
    <tabbarItem path="/profile">
      <img src="~assets/img/tabbar/profile.svg" slot="item-icon">
      <img src="~assets/img/tabbar/profile_active.svg" slot="item-icon-active">
      <div slot="item-text">我的</div>
    </tabbarItem>
    </tabbar>
  </div>
</template>

<script>
import tabbar from 'components/common/tabbar/tabbar'
import tabbarItem from 'components/common/tabbar/tabbar-item'

export default {
  name:'maintabbar',
  components:{
    tabbar,
    tabbarItem
  }
}
</script>

<style>

</style>