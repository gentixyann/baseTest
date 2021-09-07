<template>
<div class="container">
   <div class="row mb-4">
    <div class="text-center col">
      <div class="page-container">
        <img
          src="/img/start.JPG"
          class="mb-4 contentImg"
          v-if="!start"
        >
        <div class="intro" v-if="!start">
            <h4>回答に当たっての注意点</h4>
            <ul>
                <li>すべての内容に合意できなくても、ほかの2つの文章よりも自分に当てはまるものを直感的に選択して下さい。</li>
                <li>こうありたい自分ではなく、これまでの人生の大半において実際にそうだったという傾向をお答え下さい。</li>
                <li>疲れている時など、通常の状態でない時に回答するのは、お勧めしません。</li>
            </ul>
        </div>
        <!--pageNumで問題を分割-->
        <question :question="questions[pageNum]" v-if="start"></question>
      </div>
    </div>
  </div>
  <div class="row" v-if="!start">
    <div class="text-center col">
     <button class="startBtn" @click="start = true">診断スタート</button>
    </div>
  </div>
  <div class="row" v-else>
    <button class="col-sm-4 btnA" @click="next(0)" type="button">A</button>
    <button class="col-sm-4 btnB" @click="next(1)" type="button">B</button>
    <button class="col-sm-4 btnC" @click="next(2)" type="button">C</button>
    <button @click="back">back</button><!--戻るボタン(ノリで作成)-->
  </div>
</div>
</template>

<script>
import {questions} from '~/assets/js/data.js'
const Question = () => import('../components/questions/Question.vue');
export default {
  components: {
    Question
  },
  data() {
    return {
      start: false,
      pageNum: 0,
      answers: '',
    }
  },
  computed: {
    //data.jsからimportした問題のデータをquestionコンポーネントに流し込む
    questions() {
      return questions;
    }
  },
  methods: {
    next(answer) {
      //回答するたびに文字列が足されていく "0"->"02"
      this.answers +=  String(answer);
      // lastpageかどうか判定
      const lastPage = this.pageNum == this.questions.length-1;
      // lastPageならresult()、そうでないならpageNumに+1
      lastPage ? this.result() : this.pageNum += 1;
    },
    back() {
      //前回の回答をなしにする(最後の文字列削除)
      this.answers = this.answers.slice(0, -1);
      //最初の診断スタートページに戻る
      if (this.pageNum == 0) this.start = false;
      //ひとつ前の質問に戻る
      else this.pageNum -= 1;
    },
    result() {
      //回答のkeyを結果ページに送る 例->"02"
      this.$router.push({ name: 'result-final', params: { answerKey: this.answers } })
    }
  }
}
</script>

<style scoped>
.intro {
    background: #eaf3ff;
    padding: 10px;
    border-radius: 40px;
}
.startBtn {
    background: #8fc3ff;
    border-radius: 80px;
    box-shadow: 0px 2px 5px #8fc3ff;
    font-weight: 700;
    height: 49px;
    width: 240px;
    max-width: 100%;
}
.btnA {
    background: #8fc3ff;
    border-radius: 80px;
    box-shadow: 0px 2px 5px #8fc3ff;
    font-weight: 700;
    height: 49px;
    width: 240px;
    max-width: 100%;
}
.btnB {
    background: #8fc3ff;
    border-radius: 80px;
    box-shadow: 0px 2px 5px #8fc3ff;
    font-weight: 700;
    height: 49px;
    width: 240px;
    max-width: 100%;
}
.btnC {
    background: #8fc3ff;
    border-radius: 80px;
    box-shadow: 0px 2px 5px #8fc3ff;
    font-weight: 700;
    height: 49px;
    width: 240px;
    max-width: 100%;
}
</style>

