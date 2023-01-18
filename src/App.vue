<template>
  <v-app>
    <the-header></the-header>
    <v-main>
      <v-container>
        <v-row>
          <v-col cols="12">
            <booking></booking>
          </v-col>
          <v-col cols="12">
            <statistics></statistics>
          </v-col>
          <v-col cols="12">
            <column-chart></column-chart>
          </v-col>
          <v-col cols="12">
            <vertical-bar></vertical-bar>
          </v-col>
          <v-col cols="12">
            <pie-chart></pie-chart>
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
import ColumnChart from "./components/Charts/ColumnChart";
import Statistics from "./components/Statistics";
import Booking from "./components/Booking";
export default {
  name: "App",

  components: {
    TheHeader,
    VerticalBar,
    PieChart,
    ColumnChart,
    Statistics,
    Booking,
  },
};
</script>
<style>
.theme--light.v-application {
    background: rgb(228, 228, 228);
}
</style>