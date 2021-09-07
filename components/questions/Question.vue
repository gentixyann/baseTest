<template>
    <div>
        <!--質問表示-->
        <h2>{{question.title}}</h2>
        <div>
            <!--選択肢answersをfor文で回す-->
          <p v-for="(answer, i) in question.answers" :key="i">
              <!--回答の選択肢を表示-->
              {{ initial[i] }}. {{ answer.text }}
          </p>
        </div>
    </div>
</template>

<script lang="ts">
import Vue from 'vue'
export default Vue.extend({
    // index.vueから受け取ったquestionをpropsで受け取る
    // questionはdata.jsの問題１つ分
    props: ['question'],
    computed: {
        //選択肢の数だけinitialにA,B,Cと自動でつく
        initial() {
            return [...Array(this.question.answers.length)].map((v, i) => String.fromCodePoint(i + 65));
        }
    }
})
</script>
