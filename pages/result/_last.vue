<template>
<v-container>
  <v-row>
    <v-col class="text-center">
       {{ $route.params.id }}点！
        <p>「Yes」で+1「No」で+0</p>
    </v-col>
  </v-row>
    <div v-if="resultsNum == 0">
      <p>ズバリ0ですね！</p>
      <Result1 />
    </div>
    <div v-else-if="resultsNum>=1 && resultsNum<=3">
      <p>ズバリ１〜３ですね！</p>
       <Result2 />
    </div>
    <div v-else-if="resultsNum>=4 && resultsNum<=5">
      <p>ズバリ4〜5ですね！</p>
      <Result3 />
    </div>
  <v-row>
    <v-col class="text-center">
      <nuxt-link to="/">Topへ戻る</nuxt-link>
    </v-col>
  </v-row>
</v-container>
</template>

<script lang="ts">
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
      resultsNum: Number(this.$route.params.id),
    }
  },
  computed: {

  }
})
</script>



