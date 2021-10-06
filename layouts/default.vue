<template>
  <div class="wrapper">
    <LoadingScreen :isLoading="isLoading" />
    <transition name="fade" v-if="!isLoading">
      <Nuxt v-if="ready" />
    </transition>
    <footer class="mt-4">
      <div class="text-center p-2">&copy; {{ new Date().getFullYear() }}</div>
    </footer>
  </div>
</template>

<script>
const LoadingScreen = () => import("../components/LoadingScreen.vue");
export default {
  components: {
    LoadingScreen,
  },
  data() {
    return {
      ready: false,
      isLoading: true,
    };
  },
  mounted() {
    this.ready = true;
    setTimeout(() => {
      this.isLoading = false;
    }, 1000);
  },
};
</script>
