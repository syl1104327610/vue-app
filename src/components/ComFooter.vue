<template>
  <footer :style="{ backgroundColor:curMenu.bgColor}">
    <div v-for="menu in menuList" :key="menu.path" @click="switchMenu(menu)">
      <router-link :to="menu.path">{{ menu.name }}</router-link>
    </div>
  </footer>
</template>

<script>
import { mapState, mapMutations } from "vuex";
export default {
  computed: {
    ...mapState(["curMenu"]),
  },
  data() {
    return {
      menuList: [
        { path: "/", name: "剧集",  bgColor: "#8c00ff" },
        { path: "/music", name: "音乐", bgColor: "#00ff77" },
        { path: "/book", name: "书籍", bgColor: "#ff0080" },
        { path: "/chat", name: "聊天", bgColor: "#0084ff" },
      ],
    };
  },
  methods: {
    ...mapMutations(["setCurMenu"]),
    switchMenu(menu) {
      this.setCurMenu(menu);
    },
  },
};
</script>

<style lang="scss" scoped>
footer {
  display: flex;
  justify-content: space-around;
  height: 1rem;
  width: 100%;
  text-align: center;
  line-height: 1rem;
  background: cornflowerblue;
  position: fixed;
  bottom: 0;
}
</style>