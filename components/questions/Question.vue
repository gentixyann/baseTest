<template>
  <div class="mt-5">
    <!--質問表示-->
    <h2>{{ question.title }}</h2>
    <img
      :src="require(`@/assets/images/questions/${question.img}`)"
      class="mb-4 contentImg"
    />
    <div class="answerText">
      <!--選択肢answersをfor文で回す-->
      <div class="text-left" style="display: inline-block">
        <p v-for="(answer, i) in question.answers" :key="i" class="mb-2" style="inline-block">
          <!--回答の選択肢を表示-->
          <span class="mr-2">{{ initial[i] }}</span>
          {{ answer.text }}
        </p>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from "vue";
export default Vue.extend({
  // index.vueから受け取ったquestionをpropsで受け取る
  // questionはdata.jsの問題１つ分
  props: ["question"],
  computed: {
    //選択肢の数だけinitialにA,B,Cと自動でつく
    initial() {
      return [...Array(this.question.answers.length)].map((v, i) =>
        String.fromCodePoint(i + 65)
      );
    },
  },
});
</script>

<style scoped>
.answerText span {
  display: inline-block;
  width: 35px;
  height: 35px;
  border-radius: 50%;
  text-align: center;
  line-height: 35px;
  border: 1px solid;
}
.answerText p:nth-child(1) span {
  background: #ffdede;
  box-shadow: 0px 2px 5px #ffdede;
}
.answerText p:nth-child(2) span {
  background: #f7f3ce;
  box-shadow: 0px 2px 5px #f7f3ce;
}
.answerText p:nth-child(3) span {
  background: #c5ecbe;
  box-shadow: 0px 2px 5px #c5ecbe;
}
</style>
