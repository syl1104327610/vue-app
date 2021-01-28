<template>
  <div>
    <ul>
      <li
        class="main"
        v-for="tv in tvList"
        :key="tv.id"
        @click="getText(tv.id)"
      >
        <div class="img-box">
          <img :src="'https://images.weserv.nl/?url=' + tv.cover.url" alt="" />
        </div>
        <div class="content">
          <h3>{{ tv.title }}</h3>
          <p>{{ tv.info }}</p>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "Tv",
  created() {
    this.getData();
  },
  mounted() {
    this.lazyLoad();
  },
  data() {
    return {
      tvList: [],
      start: 0,
      isFinish: true,
    };
  },
  methods: {
    getData() {
      if (this.isFinish) {
        (this.isFinish = false),
          this.axios
            .get(
              "https://bird.ioliu.cn/v2?url=https://m.douban.com/rexxar/api/v2/subject_collection/tv_domestic/items",
              {
                params: {
                  start: this.start,
                  count: 10,
                },
              }
            )
            .then((res) => {
              this.tvList = [
                ...this.tvList,
                ...res.data.subject_collection_items,
              ];
              this.isFinish = true;
            });
      }
    },
    lazyLoad() {
      let htmlDom = document.documentElement;
      let fullHeight = 0;
      let deviceHeight = htmlDom.clientHeight;
      let scrollT = 0;
      window.onscroll = () => {
        fullHeight = htmlDom.offsetHeight;
        scrollT = htmlDom.scrollTop;
        if (fullHeight == deviceHeight + scrollT) {
          if (this.start < 40) {
            this.start += 10;
            this.getData();
          }
        }
      };
    },
    getText(id) {
      this.$router.push('/tvText/'+id)
    },
  },
};
</script>

<style lang="scss" scoped>
.main {
  display: flex;
  padding: 0.2rem 0;
  border-bottom: dashed 1px #ccc;
  .img-box {
    flex: 3;
    img {
      width: 100%;
      height: 100%;
    }
  }
  .content {
    flex: 5;
    text-align: center;
    display: flex;
    flex-direction: column;
    justify-content: space-around;
    padding: 0.8rem;
    h3 {
      font-weight: bold;
    }
  }
}
</style>