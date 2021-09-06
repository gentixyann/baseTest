<template>
    <div>
        <h2>{{question.title}}</h2>
        <div>
          <p v-for="(answer, i) in question.answers" :key="i">{{initial[i]}}. {{answer.text}}</p>
        </div>
    </div>
</template>

<script lang="ts">
import Vue from 'vue'
export default Vue.extend({
    props: ['question'],
    data() {
        return {
            initial: ['A', 'B', 'C']
        }
    }
})
</script>