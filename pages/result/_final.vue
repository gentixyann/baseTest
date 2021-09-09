<template>
<div class="container">
  <div class="row">
    <div class="text-center col">
       {{ result }}点！
    </div>
  </div>

  <div class="row">
    <div class="text-center col">
      <nuxt-link to="/">Topへ戻る</nuxt-link>
    </div>
  </div>
</div>
</template>

<script lang="ts">
import { resultsData } from '~/assets/js/data.js'
import Vue from 'vue'
interface DataType { answerKey: string | null }

export default Vue.extend({
  data(): DataType {
    return {
      answerKey: null,
    }
  },
  computed: {
    result() {
      //index.vueから送られてきたanswerKeyを元に結果を検索しresultにバインディング
      return resultsData.find((result: {id: string}) => result.id == (this as any).answerKey);
    }
  },
  //angularにもある？ある値の変化を検知
  watch: {
    //vue-router.ページがリロードされたり、queryなどが変わったら検知
    '$route': {
      handler(from, to) {
        //$routeのparamsにanswerKeyが入ってた場合
        if('answerKey' in from.params) {
          //dataのanswerKeyに格納
          this.answerKey = this.$route.params.answerKey;
          //sessionstorageにも格納(リロードされた場合this.$route.params.answerKeyが消失しエラーになるため)
          // 本番では本番のURLにする
          sessionStorage.setItem('localhost:3000', this.answerKey);
        } else {
          // result画面でリロードした時sessionStorageを読み込む
          this.answerKey = sessionStorage.getItem('localhost:3000');
          //故意に消された場合topに戻す
          if(!this.answerKey) this.$router.push('/');
        }
      },
      // result画面に来てすぐwatchの$routeを検知
      immediate: true
    }
  }
})
</script>

<style scoped>

</style>



