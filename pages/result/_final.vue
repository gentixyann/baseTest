<template>
<div class="container">
  <div class="row">
    <div class="text-center col">
       {{ result }}点！
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
import {results} from '~/assets/js/data.js'
import Vue from 'vue'
interface DataType {answerKey: string | null}

export default Vue.extend({
  data(): DataType {
    return {
      answerKey: null,
    }
  },
  computed: {
    result() {
      return results.find((result: {id: string}) => result.id == (this as any).answerKey)
    }
  },
  watch: {
    '$route': {
      handler(from, to) {
        if('answerKey' in from.params) {
          this.answerKey = this.$route.params.answerKey;
          sessionStorage.setItem('localhost:3000', this.answerKey);
        } else {
          this.answerKey = sessionStorage.getItem('localhost:3000')
        }
      },
      immediate: true
    }
  }
})
</script>

<style scoped>

</style>



