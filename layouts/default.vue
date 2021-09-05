<template>
  <v-app>
    <v-main>
      <v-container>
        <Nuxt />
      </v-container>
    </v-main>
    <v-footer
      class="text-center"
      absolute
      color="primary lighten-3"
    >
    <div class="footer">
       &copy; {{ new Date().getFullYear() }}
    </div>
    </v-footer>
  </v-app>
</template>

<script>
export default {

}
</script>

