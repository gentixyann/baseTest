<template>
<div class="container">
  <div class="row">
    <div class="text-center col">
       {{ $route.params.array }}点！
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
    }
  },
  computed: {

  }
})
</script>

<style scoped>

</style>



