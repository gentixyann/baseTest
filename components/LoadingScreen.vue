<template>
  <div :class="{ loader: true, fadeout: !isLoading }">
    <div class="text-center">
      <img src="@/assets/images/type/main_type1.png" class="contentImg" />
    </div>
  </div>
</template>

<script lang="ts">
import Vue from "vue";
export default Vue.extend({
  name: "LoadingScreen",
  props: ["isLoading"],
});
</script>

<style scoped>
.loader {
  background-color: #ffffff;
  bottom: 0;
  color: white;
  display: block;
  font-size: 32px;
  left: 0;
  overflow: hidden;
  padding-top: 10vh;
  position: fixed;
  right: 0;
  text-align: center;
  top: 0;
}

.fadeout {
  animation: fadeout 2s forwards;
}

@keyframes fadeout {
  to {
    opacity: 0;
    visibility: hidden;
  }
}
</style>
