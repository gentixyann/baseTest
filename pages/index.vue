<template>
<v-container>
   <v-row>
    <v-col class="text-center">
      <div class="page-container">
        <img
          src="/img/start.JPG"
          class="mb-5 contentImg"
          v-if="!start"
        >
        <div :is="components" v-if="start"></div>
        {{ answer }}
      </div>
    </v-col>
  </v-row>
  <v-row>
    <v-col class="text-center">
     <v-btn v-if="!start" @click="start = true">診断スタート</v-btn>
     <div v-else>
       <v-btn @click="next(1)" color="indigo">Yes</v-btn>
       <v-btn @click="next(0)" color="red">No</v-btn>
     </div>
    </v-col>
  </v-row>
</v-container>
</template>

<script>
const Question1 = () => import('../components/questions/Question1.vue');
const Question2 = () => import('../components/questions/Question2.vue');
const Question3 = () => import('../components/questions/Question3.vue');
const Question4 = () => import('../components/questions/Question4.vue');
const Question5 = () => import('../components/questions/Question5.vue');
export default {
  components: {
    Question1,
    Question2,
    Question3,
    Question4,
    Question5
  },
  data() {
    return {
      start: false,
      pageNum: 0,
      answers: [],
      componentTypes: [
        'question1',
        'question2',
        'question3',
        'question4',
        'question5',
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
      this.$router.push({ name: 'result-last', params: { id: points } })
    }
  }
}
</script>

<style scoped>

</style>

