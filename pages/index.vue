<template>
  <div class="container">
    <div class="page-container mb-4 text-center">
      <transition name="fade" mode="out-in">
        <div key="1" v-if="!start">
          <img
            src="@/assets/images/start.JPG"
            class="mb-4 contentImg"
            v-if="!start"
          />
          <div class="intro mb-4">
            <h4>回答に当たっての注意点</h4>
            <ul>
              <li>
                すべての内容に合意できなくても、ほかの2つの文章よりも自分に当てはまるものを直感的に選択して下さい。
              </li>
              <li>
                こうありたい自分ではなく、これまでの人生の大半において実際にそうだったという傾向をお答え下さい。
              </li>
              <li>
                疲れている時など、通常の状態でない時に回答するのは、お勧めしません。
              </li>
            </ul>
          </div>
          <div class="row">
            <div class="text-center col">
              <button class="startBtn" @click="start = true">
                診断スタート
              </button>
            </div>
          </div>
        </div>
        <!-- pageNumで問題を分割しquestionとしてQuestion.vueに渡す -->
        <div key="2" v-else>
          <transition name="fade" mode="out-in">
            <div v-if="show">
              <div>
                <Question :question="questions[pageNum]"></Question>
              </div>
              <div>
                <div class="row answerBtn justify-content-center">
                  <button class="col-sm-3 btnA" @click="next(0)" type="button">
                    A
                  </button>
                  <button class="col-sm-3 btnB" @click="next(1)" type="button">
                    B
                  </button>
                  <button class="col-sm-3 btnC" @click="next(2)" type="button">
                    C
                  </button>
                </div>
                <div class="text-center mt-5">
                  <button class="backBtn" @click="back">
                    <span>前の質問に戻る</span>
                  </button>
                </div>
              </div>
            </div>
          </transition>
        </div>
      </transition>
    </div>
  </div>
</template>




<script>
import { questionsData } from "@/assets/js/data.js";
const Question = () => import("../components/questions/Question.vue");
export default {
  components: {
    Question,
  },
  data() {
    return {
      start: false,
      pageNum: 0,
      answers: "",
      show: true,
    };
  },
  computed: {
    //data.jsからimportした問題のデータをquestionコンポーネントに流し込む
    questions() {
      return questionsData;
    },
  },
  methods: {
    next(answer) {
      this.show = false;
      setTimeout(() => {
        //回答するたびに文字列が足されていく "0"->"02"
        this.answers += String(answer);
        // lastpageかどうか判定
        const lastPage = this.pageNum == this.questions.length - 1;
        // lastPageならresult()、そうでないならpageNumに+1
        lastPage ? this.result() : (this.pageNum += 1);
        this.show = true
      }, 2000);
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
      this.$router.push({
        name: "result-final",
        params: { answerKey: this.answers },
      });
    },
  },
};
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
.answerBtn button {
  margin: 10px;
}
.btnA {
  background: #ffdede;
  border-radius: 80px;
  box-shadow: 0px 2px 5px #ffdede;
  font-weight: 700;
  height: 49px;
  width: 240px;
  max-width: 100%;
}
.btnB {
  background: #f7f3ce;
  border-radius: 80px;
  box-shadow: 0px 2px 5px #f7f3ce;
  font-weight: 700;
  height: 49px;
  width: 240px;
  max-width: 100%;
}
.btnC {
  background: #c5ecbe;
  border-radius: 80px;
  box-shadow: 0px 2px 5px #c5ecbe;
  font-weight: 700;
  height: 49px;
  width: 240px;
  max-width: 100%;
}
.backBtn {
  display: inline-block;
  width: 200px;
  line-height: 58px;
  color: #4f2513;
  font-size: 16px;
  font-weight: 600;
  background-color: #fff;
  border-radius: 10px;
  box-shadow: 0 3px #ccc;
  position: relative;
}
.backBtn ::before {
  content: "";
  display: inline-block;
  height: 20px;
  width: 20px;
  background-image: url("~@/assets/images/back_img.png");
  background-size: cover;
  position: absolute;
  left: 20px;
  top: 50%;
  margin-top: -10px;
}
.backBtn span {
  margin-left: 20px;
}
</style>

