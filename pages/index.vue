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
        <div :is="components" v-if="start"></div>
        <!-- {{ answers }} -->
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
  </div>
</div>
</template>

<script>
const Question1 = () => import('../components/questions/Question1.vue');
const Question2 = () => import('../components/questions/Question2.vue');

export default {
  components: {
    Question1,
    Question2,
  },
  data() {
    return {
      start: false,
      pageNum: 0,
      answers: [],
      componentTypes: [
        'question1',
        'question2',
      ]
    }
  },
  computed: {
    components() {
      return this.componentTypes[this.pageNum];
    }
  },
  // 初期化で大体使うやつ
  created() {
  this.answers = new Array(this.componentTypes.length)
    .fill(0)
  },
  methods: {
    next(answer) {
      this.answers[this.pageNum] += answer;
      const lastPage = this.pageNum == this.componentTypes.length-1;
      // lastPageならresult()、そうでないならpageNumに+1
      lastPage ? this.result() : this.pageNum += 1;
    },
    result() {
      // reduceでanswers配列内の数値を全て足す
      const points = this.answers.reduce((a, b) => a + b, 0);
    //   this.$router.push({ name: 'result-last', params: { id: points } });
      this.$router.push({ name: 'result-final', params: { array: this.answers } })
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

