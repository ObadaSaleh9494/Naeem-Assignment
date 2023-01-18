<template>
  <v-row>
    <v-col cols="12" lg="6">
      <v-card class="mx-auto" color="success" dark max-width="400">
        <v-card-title>
          <v-icon large left> mdi-swap-vertical-circle-outline </v-icon>
          <span class="title font-weight-light">Number of Total Bookings </span>
        </v-card-title>

        <v-card-text class="headline font-weight-bold text-center">
          {{ data.length }}
        </v-card-text>
      </v-card>
    </v-col>
    <v-col cols="12" lg="6">
      <v-card class="mx-auto" color="success" dark max-width="400">
        <v-card-title>
          <v-icon large left> mdi-swap-vertical-circle-outline </v-icon>
          <span class="title font-weight-light">Total Price</span>
        </v-card-title>

        <v-card-text class="headline font-weight-bold text-center">
          {{ total_price }}
        </v-card-text>
      </v-card>
    </v-col>
  </v-row>
</template>

<script>
import { data } from "../database";
export default {
  data() {
    return {
      data,
    };
  },
  computed: {
    total_price() {
      const sum = this.data.reduce((accumulator, object) => {
        return accumulator + parseInt(object.price);
      }, 0);
      return sum;
    },
  },
};
</script>

<style></style>
