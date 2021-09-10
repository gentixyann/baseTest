<template>
  <div class="container">
    <div class="page-container mb-4 mt-5 text-center">
      <h4 class="resultHeadline">
        <span>ズバリあなたは</span>
      </h4>
      <h2 class="mt-5">{{ result.text }}</h2>
      <div class="mt-3">
        <img
          :src="require(`@/assets/images/type/${result.img}`)"
          class="contentImg"
        />
      </div>
    </div>

    <div class="row">
      <div class="text-center col">
        <nuxt-link to="/">
          <button class="backToTop">Topへ戻る</button>
        </nuxt-link>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { resultsData } from "~/assets/js/data.js";
import Vue from "vue";
interface DataType {
  answerKey: string | null;
}

export default Vue.extend({
  data(): DataType {
    return {
      answerKey: null,
    };
  },
  computed: {
    result() {
      //index.vueから送られてきたanswerKeyを元に結果を検索しresultにバインディング
      return resultsData.find(
        (result: { id: string }) => result.id == (this as any).answerKey
      );
    },
  },
  //angularにもある？ある値の変化を検知
  watch: {
    //vue-router.ページがリロードされたり、queryなどが変わったら検知
    $route: {
      handler(from, to) {
        //$routeのparamsにanswerKeyが入ってた場合
        if ("answerKey" in from.params) {
          //dataのanswerKeyに格納
          this.answerKey = this.$route.params.answerKey;
          //sessionstorageにも格納(リロードされた場合this.$route.params.answerKeyが消失しエラーになるため)
          // 本番では本番のURLにする
          sessionStorage.setItem("basetest-22450.web.app", this.answerKey);
        } else {
          // result画面でリロードした時sessionStorageを読み込む
          this.answerKey = sessionStorage.getItem("localhost:3000");
          //故意に消された場合topに戻す
          if (!this.answerKey) this.$router.push("/");
        }
      },
      // result画面に来てすぐwatchの$routeを検知
      immediate: true,
    },
  },
});
</script>

<style scoped>
.resultHeadline {
  font-size: 20px;
  position: relative;
}
.resultHeadline::after {
  content: "";
  display: block;
  width: 100px;
  height: 4px;
  background-color: #f3e1f3;
  position: absolute;
  left: 0;
  right: 0;
  bottom: -9px;
  margin: auto;
}
.backToTop {
  height: 49px;
  width: 240px;
  border-radius: 80px;
  border: 1px solid #cccccc;
  background-color: #ffffff;
  color: #666;
}
</style>



