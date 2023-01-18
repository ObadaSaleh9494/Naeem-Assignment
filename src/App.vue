<template>
  <v-app>
    <the-header></the-header>
    <v-main>
      <v-container>
        <v-row>
          <v-col cols="12">
            <statistics></statistics>
          </v-col>
          <v-col cols="12">
            <booking></booking>
          </v-col>
        </v-row>
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
import Booking from "./components/Booking";
import Statistics from "./components/Statistics";
import TheHeader from "./layouts/TheHeader";
export default {
  name: "App",

  components: {
    TheHeader,
    Statistics,
    Booking,
  },
};
</script>
