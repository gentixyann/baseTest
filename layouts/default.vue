<template>
  <div class="wrapper">
    <transition name="fade">
      <Nuxt v-if="ready" />
    </transition>
    <footer class="mt-4">
      <div class="text-center p-2">&copy; {{ new Date().getFullYear() }}</div>
    </footer>
  </div>
</template>

<script>
export default {
  data() {
    return {
      ready: false,
    };
  },
  mounted() {
    this.ready = true;
  },
};
</script>
