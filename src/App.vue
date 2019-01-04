<template>
  <div id="app">
    <router-view></router-view>
    <FooterGuide/>
  </div>
</template>

<script>
import FooterGuide from "./components/FooterGuider/FooterGuider.vue";
import { mapActions } from "vuex";
export default {
  mounted() {
    this.$store.dispatch("getAddress");
  },
  methods: {
    ...mapActions(["getAddress"])
  },
  components: {
    FooterGuide
  }
};
</script>

<style lang="stylus">
.app
  width 100%
  height 100%
  background #f5f5f5
</style>

