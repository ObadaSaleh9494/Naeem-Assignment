<template>
  <td :colspan="headers.length">
    <v-row dense class="pa-2 align-center">
      <v-col cols="12" lg="4">
        <v-list-item two-line>
          <v-list-item-content>
            <v-list-item-title>Arrival Date Year</v-list-item-title>
            <v-list-item-subtitle>{{
              item.arrival_date_year
            }}</v-list-item-subtitle>
          </v-list-item-content>
        </v-list-item>
        <v-list-item two-line>
          <v-list-item-content>
            <v-list-item-title>Arrival Date Month</v-list-item-title>
            <v-list-item-subtitle>{{
              item.arrival_date_month
            }}</v-list-item-subtitle>
          </v-list-item-content>
        </v-list-item>
        <v-list-item two-line>
          <v-list-item-content>
            <v-list-item-title>Arrival Date Week Number</v-list-item-title>
            <v-list-item-subtitle>{{
              item.arrival_date_week_number
            }}</v-list-item-subtitle>
          </v-list-item-content>
        </v-list-item>
        <v-list-item two-line>
          <v-list-item-content>
            <v-list-item-title>Arrival Date Day Of Month</v-list-item-title>
            <v-list-item-subtitle>{{
              item.arrival_date_day_of_month
            }}</v-list-item-subtitle>
          </v-list-item-content>
        </v-list-item>
        <v-list-item two-line>
          <v-list-item-content>
            <v-list-item-title>Stays In Weekend Nights</v-list-item-title>
            <v-list-item-subtitle>{{
              item.stays_in_weekend_nights == 1 ? "Yes" : "No"
            }}</v-list-item-subtitle>
          </v-list-item-content>
        </v-list-item>
      </v-col>
      <v-col cols="12" lg="4">
        <v-list-item two-line>
          <v-list-item-content>
            <v-list-item-title>Stays In Week Nights</v-list-item-title>
            <v-list-item-subtitle>{{
              item.stays_in_week_nights == 1 ? "Yes" : "No"
            }}</v-list-item-subtitle>
          </v-list-item-content>
        </v-list-item>
        <v-list-item two-line>
          <v-list-item-content>
            <v-list-item-title>Children</v-list-item-title>
            <v-list-item-subtitle>{{
              parseInt(item.children)
            }}</v-list-item-subtitle>
          </v-list-item-content>
        </v-list-item>
        <v-list-item two-line>
          <v-list-item-content>
            <v-list-item-title>Babies</v-list-item-title>
            <v-list-item-subtitle>{{ item.babies }}</v-list-item-subtitle>
          </v-list-item-content>
        </v-list-item>
        <v-list-item two-line>
          <v-list-item-content>
            <v-list-item-title>Reservation Status Date</v-list-item-title>
            <v-list-item-subtitle>{{
              item.reservation_status_date
            }}</v-list-item-subtitle>
          </v-list-item-content>
        </v-list-item>
        <v-list-item two-line>
          <v-list-item-content>
            <v-list-item-title>Credit Card</v-list-item-title>
            <v-list-item-subtitle>{{ item.credit_card }}</v-list-item-subtitle>
          </v-list-item-content>
        </v-list-item>
      </v-col>
      <v-col cols="12" lg="4">
        <v-list-item two-line>
          <v-list-item-content>
            <v-list-item-title>Is Repeated Guest</v-list-item-title>
            <v-list-item-subtitle>{{
              item.is_repeated_guest == 1 ? "Yes" : "No"
            }}</v-list-item-subtitle>
          </v-list-item-content>
        </v-list-item>
        <v-list-item two-line>
          <v-list-item-content>
            <v-list-item-title>Reserved Room Type</v-list-item-title>
            <v-list-item-subtitle>{{
              item.reserved_room_type
            }}</v-list-item-subtitle>
          </v-list-item-content>
        </v-list-item>
        <v-list-item two-line>
          <v-list-item-content>
            <v-list-item-title>Deposit Type</v-list-item-title>
            <v-list-item-subtitle>{{ item.deposit_type }}</v-list-item-subtitle>
          </v-list-item-content>
        </v-list-item>
        <v-list-item two-line>
          <v-list-item-content>
            <v-list-item-title>Customer Type</v-list-item-title>
            <v-list-item-subtitle>{{
              item.customer_type
            }}</v-list-item-subtitle>
          </v-list-item-content>
        </v-list-item>
        <v-list-item two-line>
          <v-list-item-content>
            <v-list-item-title>Meal</v-list-item-title>
            <v-list-item-subtitle>{{ item.meal }}</v-list-item-subtitle>
          </v-list-item-content>
        </v-list-item>
      </v-col>
    </v-row>
  </td>
</template>

<script>
export default {
  props: {
    headers: [Array, Object],
    item: [Object, Array],
  },
};
</script>

<style></style>
