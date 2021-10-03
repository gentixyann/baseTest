<template>
  <div class="mt-5">
    <!--質問表示-->
    <div class="text-center">
      <h2>{{ question.title }}</h2>
      <img
        :src="require(`@/assets/images/questions/${question.img}`)"
        class="mb-4 contentImg"
      />
    </div>
    <div class="answersText">
      <!--選択肢answersをfor文で回す-->
      <div
        v-for="(answer, i) in question.answers"
        :key="i"
        class="mb-2 d-flex answerText"
      >
        <!--回答の選択肢を表示-->
        <div class="circle mr-2">
          <p>{{ initial[i] }}</p>
        </div>
        <div class="answer">
          <p>{{ answer.text }}</p>
        </div>
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
.circle {
  width: 35px;
  height: 35px;
  border-radius: 50%;
  text-align: center;
  line-height: 35px;
  border: 1px solid;
  flex-shrink: 0;
}

.answersText .answerText:nth-child(1) .circle {
  background: #ffdede;
  box-shadow: 0px 2px 5px #ffdede;
}
.answersText .answerText:nth-child(2) .circle {
  background: #f7f3ce;
  box-shadow: 0px 2px 5px #f7f3ce;
}
.answersText .answerText:nth-child(3) .circle {
  background: #c5ecbe;
  box-shadow: 0px 2px 5px #c5ecbe;
}
</style>
