<template>
  <v-app>
    <the-header></the-header>
    <v-main>
      <v-container>
        <v-row>
          <v-col cols="12">
            <vertical-bar></vertical-bar>
          </v-col>
          <v-col cols="12">
            <pie-chart></pie-chart>
          </v-col>
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
import TheHeader from "./layouts/TheHeader";
import VerticalBar from "./components/Charts/VerticalBar";
import PieChart from "./components/Charts/PieChart";
import Statistics from "./components/Statistics";
import Booking from "./components/Booking";
export default {
  name: "App",

  components: {
    TheHeader,
    VerticalBar,
    PieChart,
    Statistics,
    Booking,
  },
};
</script>
