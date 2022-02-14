<template>
  <nav>
    <router-link to="/Money" class="item" active-class="selected">
      <!--      <Icon name="money"/>-->
      <i class="iconfont icon-fukuan"></i>
      <span>记账</span>
    </router-link>
    <router-link to="/Labels" class="item" active-class="selected">
      <!--      <Icon name="labels"/>-->
      <i class="iconfont icon-faxian"></i>
      <span>标签</span>
    </router-link>
    <router-link to="/Statistics" class="item" active-class="selected">
      <!--      <Icon name="statistics"/>-->
      <i class="iconfont icon-gaishuai"></i>
      <span>统计</span>
    </router-link>
  </nav>
</template>

<script lang="ts">
export default {
  name: 'Nav'
};
</script>

<style lang="scss" scoped>
@import "~@/assets/style/helper.scss";

nav {
  background-color: #fff;
  box-shadow: 0 0 3px #ccc;
  display: flex;
  justify-content: space-around;

  > .item {
    padding: 2px 0;
    width: 33.333%;
    display: flex;
    color: #666;
    justify-content: center;
    align-items: center;
    flex-direction: column;

    i {
      display: block;
      font-size: 2rem;
      color: inherit;
    }

    //.icon {
    //  width: 32px;
    //  height: 32px;
    //}

    span {
      font-weight: 600;
    }
  }

  > .item.selected {
    color: $themeColor;
  }
}
</style>