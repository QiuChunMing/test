<template>
  <div>
    <header class="header">
      <slot class="left"></slot>
      <span class="header_title">
        <span class="header_title_text ellipsis">{{title}}</span>
      </span>
      <slot class="right"></slot>
    </header>
  </div>
</template>

<script>

export default {
  props: {
    title: String
  },
  methods: {
  }
};
</script>
<style lang="stylus">
.header
  background-color #02a774
  position fixedz-index 100
  left 0
  right 0
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
      color #ffffff
  .header_title
    position absolute
    top 50%
    left 50%
    transform translate(-50%, -50%)
    width 50%
    color #ffffff
    text-align center
    .header_title_text
      font-size 20px
      color #ffffff
      display block
  .header_login
    font-size 14px
    color #ffffff
    position absolute
    right 15px
    top 50%
    transform translateY(-50%)
    .header_login_text
      color #ffffff
</style>
