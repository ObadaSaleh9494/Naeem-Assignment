<template>
  <v-app>
    <the-header></the-header>
    <v-main>
      <v-container> <booking></booking></v-container>
    </v-main>
  </v-app>
</template>

<script>
import Booking from "./components/Booking";
import TheHeader from "./layouts/TheHeader";
export default {
  name: "App",

  components: {
    TheHeader,
    Booking,
  },
};
</script>
