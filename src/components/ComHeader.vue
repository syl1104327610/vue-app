<template>
  <header :style="{ backgroundColor: curMenu.bgColor }">
    <span @click="goHome">《首页</span>
    {{ curMenu.name }}
  </header>
</template>

<script>
import { mapState, mapMutations } from "vuex";
export default {
  computed: {
    ...mapState(["curMenu"]),
  },
  methods: {
    ...mapMutations(["setCurMenu"]),
    goHome() {
      this.$router.push("/"),
        this.setCurMenu({
          name: "剧集",
          bgColor: "#8c00ff",
        });
    },
  },
};
</script>

<style lang="scss" scoped>
header {
  height: 1rem;
  text-align: center;
  line-height: 1rem;
  position: fixed;
  top: 0;
  width: 100%;
  span {
    position: absolute;
    left: 0;
  }
}
</style>