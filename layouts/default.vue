<template>
  <div class="wrapper">
    <LoadingScreen :isLoading="isLoading" />
    <transition name="fade" v-if="!isLoading">
      <Nuxt />
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
      isLoading: true,
    };
  },
  mounted() {
    setTimeout(() => {
      this.isLoading = false;
    }, 1000);
  },
};
</script>
