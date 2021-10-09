<template>
  <div :class="{ loader: true, fadeout: !isLoading }">
    <div class="page-container">
      <img class="splash" src="@/assets/images/Logo.png" />
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
  display: flex;
  align-items: center;
  text-align: center;
  left: 0;
  overflow: hidden;
  position: fixed;
  right: 0;
  top: 0;
}

.splash {
  width: 150px;
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
