<template>
<div class="container">
  <div class="row">
    <div class="text-center col">
       {{ result }}点！
       <!-- {{ $route.params.array }}点！ -->
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
import {answersData} from '~/assets/data.js'
import {resultsData} from '~/assets/data.js'
import Vue from 'vue'
import Result1 from '../../components/results/Result1.vue';
import Result2 from '../../components/results/Result2.vue';
import Result3 from '../../components/results/Result3.vue';

export default Vue.extend({
components: {
  Result1,
  Result2,
  Result3,
},
  data() {
    return {
      resultsNum: this.$route.params.id,
      array: [1,1]
    }
  },
  computed: {
    result() {
      const answer1 = resultsData.find((firstAnswer) => {
        return firstAnswer.id == this.$route.params.array[0];
      })
      console.log(answer1)
      const answer2 = answer1.results.find((secondAnswer) => {
        return secondAnswer.id == this.$route.params.array[1];
      })
      return answer2
    }
  }
})
</script>

<style scoped>

</style>



