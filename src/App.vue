<template>
  <v-app>
    <the-header></the-header>
  </v-app>
</template>

<script>
import TheHeader from "./layouts/TheHeader";
export default {
  name: "App",

  components: {
    TheHeader,
  },

  data: () => ({
    //
  }),
};
</script>
