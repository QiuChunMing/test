<template>
  <section class="msite">
    <!-- 首页头部 -->
    <HeaderTop :title="address.name">
      <slot name="left">
        <span class="header_search">
          <i class="iconfont icon-sousuo"></i>
        </span>
      </slot>
      <slot name="right">
        <span class="header_login">
          <span class="header_login_text">登录|注册</span>
        </span>
      </slot>
    </HeaderTop>

    <!-- 首页导航轮播图 -->
    <nav class="msite_nav">
      <!-- Swiper容器层 -->
      <div class="swiper-container">
        <!-- Swiper包裹层 -->
        <div class="swiper-wrapper">
          <!-- 轮播div -->
          <div class="swiper-slide" v-for="(categorys, index) in categorysArr" :key="index">
            <a
              href="javascript:;"
              class="link_to_food"
              v-for="(category, index) in categorys"
              :key="index"
            >
              <div class="food_container">
                <img :src="baseImageUrl+category.image_url">
              </div>
              <span>{{category.title}}</span>
            </a>
          </div>
        </div>
      </div>
      <!-- 轮播图小圆点 -->
      <div class="swiper-pagination"></div>
    </nav>
    <!-- 首页附近商家 -->
    <ShopList></ShopList>
  </section>
</template>

<script>
import HeaderTop from "../../components/HeaderTop/HeaderTop.vue";
import ShopList from "../../components/ShopList/ShopList.vue";
import Swiper from "swiper";
import "swiper/dist/css/swiper.min.css";
import { mapState, mapActions } from "vuex";
export default {
  data() {
    return {
      baseImageUrl: "https://fuss10.elemecdn.com"
    };
  },
  mounted() {
    this.getCategorys();
    this.getShops();
  },
  methods: {
    ...mapActions(["getCategorys", "getShops"])
  },
  computed: {
    ...mapState(["address", "categorys", "shops"]),

    categorysArr() {
      const { categorys } = this;
      let slideArr = [];
      let contentArr = [];
      for (let index = 0; index < categorys.length; index++) {
        const element = categorys[index];
        if (contentArr.length === 8) {
          contentArr = [];
        }
        if (contentArr.length === 0) {
          slideArr.push(contentArr);
        }
        contentArr.push(element);
      }
      return slideArr;
    }
  },
  components: {
    HeaderTop,
    ShopList
  },
  watch: {
    categorys(value) {
      // categorys数组中有数据了，在异步更新界面之前执行
      // 希望界面更新就立即创建swiper对象
      this.$nextTick(() => {
        // 一旦界面更新立即调用(要写在数据更新之后)
        // 创建一个swiper实例对象实现轮播
        new Swiper(".swiper-container", {
          loop: true, // 循环轮播
          // 如果需要分页器
          pagination: {
            el: ".swiper-pagination"
          }
        });
      });
    }
  }
};
</script>

<style lang="stylus">
.msite // 首页
  width 100%
.header
  background-color #02a774
  position fixed
  z-index 100
  left 0
  top 0
  width 100%
  height 45px
  .header_search
    position absolute
    left 15px
    top 50%
    transform translateY(-50%)
    width 10%
    height 50%
    .icon-sousuo
      font-size 25px
      color #fff
  .header_title
    position absolute
    top 50%
    left 50%
    transform translate(-50%, -50%)
    width 50%
    color #fff
    text-align center
    .header_title_text
      font-size 20px
      color #fff
      display block
  .header_login
    font-size 14px
    color #fff
    position absolute
    right 15px
    top 50%
    transform translateY(-50%)
    .header_login_text
      color #fff
.msite_nav
  bottom-border-1px(#e4e4e4)
  margin-top 45px
  height 200px
  background #fff
  .swiper-container
    width 100%
    height 100%
    .swiper-wrapper
      width 100%
      height 100%
      .swiper-slide
        display flex
        justify-content center
        align-items flex-start
        flex-wrap wrap
        .link_to_food
          width 25%
          .food_container
            display block
            width 100%
            text-align center
            padding-bottom 10px
            font-size 0
            img
              display inline-block
              width 50px
              height 50px
          span
            display block
            width 100%
            text-align center
            font-size 13px
            color #666
    .swiper-pagination
      >span.swiper-pagination-bullet-active
        background #02a774
.msite_shop_list
  top-border-1px(#e4e4e4)
  margin-top 10px
  background #fff
  .shop_header
    padding 10px 10px 0
    .shop_icon
      margin-left 5px
      color #999
    .shop_header_title
      color #999
      font-size 14px
      line-height 20px
</style>
