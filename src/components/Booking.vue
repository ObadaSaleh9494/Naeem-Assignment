<template>
  <div class="d-flex flex-column flex-grow-1">
    <v-card>
      <v-row dense class="pa-2 align-center">
        <v-col cols="12" lg="6">
          <div class="display-1">Bookings</div>
        </v-col>
        <v-col cols="12" lg="6" class="d-flex text-right align-center">
          <v-text-field
            v-model="searchQuery"
            append-icon="mdi-magnify"
            class="flex-grow-1 mr-md-2"
            solo
            hide-details
            dense
            clearable
            placeholder="e.g. filter for id, email, name, etc"
            @keyup.enter="searchUser(searchQuery)"
          ></v-text-field>
        </v-col>
      </v-row>

      <v-data-table
        :headers="headers"
        :items="data"
        item-key="phone-number"
        show-expand
        :expanded.sync="expanded"
        :search="searchQuery"
        class="flex-grow-1"
      >
        <template v-slot:expanded-item="{ headers, item }">
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
                    <v-list-item-title
                      >Arrival Date Week Number</v-list-item-title
                    >
                    <v-list-item-subtitle>{{
                      item.arrival_date_week_number
                    }}</v-list-item-subtitle>
                  </v-list-item-content>
                </v-list-item>
                <v-list-item two-line>
                  <v-list-item-content>
                    <v-list-item-title
                      >Arrival Date Day Of Month</v-list-item-title
                    >
                    <v-list-item-subtitle>{{
                      item.arrival_date_day_of_month
                    }}</v-list-item-subtitle>
                  </v-list-item-content>
                </v-list-item>
                <v-list-item two-line>
                  <v-list-item-content>
                    <v-list-item-title
                      >Stays In Weekend Nights</v-list-item-title
                    >
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
                    <v-list-item-subtitle>{{
                      item.babies
                    }}</v-list-item-subtitle>
                  </v-list-item-content>
                </v-list-item>
                <v-list-item two-line>
                  <v-list-item-content>
                    <v-list-item-title
                      >Reservation Status Date</v-list-item-title
                    >
                    <v-list-item-subtitle>{{
                      item.reservation_status_date
                    }}</v-list-item-subtitle>
                  </v-list-item-content>
                </v-list-item>
                <v-list-item two-line>
                  <v-list-item-content>
                    <v-list-item-title>Credit Card</v-list-item-title>
                    <v-list-item-subtitle>{{
                      item.credit_card
                    }}</v-list-item-subtitle>
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
                    <v-list-item-subtitle>{{
                      item.deposit_type
                    }}</v-list-item-subtitle>
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
        <template v-slot:[`item.email`]="{ item }">
          <v-tooltip bottom>
            <template v-slot:activator="{ on }">
              <div
                class="font-weight-bold copylabel"
                v-on="on"
                @click="sendEmail(item.email)"
              >
                {{ item.email }}
              </div>
            </template>
            <span>Contact with {{ item.email }}</span>
          </v-tooltip>
        </template>
        <template v-slot:[`item.phone-number`]="{ item }">
          <v-tooltip bottom>
            <template v-slot:activator="{ on }">
              <div
                class="font-weight-bold copylabel"
                v-on="on"
                @click="call(item['phone-number'])"
              >
                {{ item["phone-number"] }}
              </div>
            </template>
            <span>Call {{ item["phone-number"] }}</span>
          </v-tooltip>
        </template>
        <template v-slot:[`item.reservation_status`]="{ item }">
          <v-chip
            label
            small
            class="font-weight-bold"
            :color="colorOfStatus(item.reservation_status)"
            >{{ item.reservation_status }}</v-chip
          >
        </template>
        <template v-slot:[`item.is_canceled`]="{ item }">
          <v-icon v-if="item.is_canceled == 1" small color="red">
            mdi-check-circle
          </v-icon>
          <v-icon v-else small> mdi-circle-outline </v-icon>
        </template>
      </v-data-table>
    </v-card>
  </div>
</template>

<script>
import { data } from "../database";

export default {
  data() {
    return {
      expanded: [],
      headers: [
        { text: "Hotel", align: "left", value: "hotel" },
        { text: "Country", value: "country" },
        { text: "Canceled?", value: "is_canceled" },
        { text: "Email", value: "email" },
        { text: "Price", value: "price" },
        { text: "Name", value: "name" },
        { text: "Phone Number", value: "phone-number" },
        { text: "Reservation Status", value: "reservation_status" },
        { text: "", value: "data-table-expand" },
      ],
      searchQuery: "",
      data,
    };
  },
  computed: {
    colorOfStatus() {
      return (reservation_status) => {
        if (reservation_status === "Check-In") return "success";
        else if (reservation_status === "Check-Out") return undefined;
        else if (reservation_status === "Canceled") return "warning";
        else if (reservation_status === "No-Show") return "cyan";
      };
    },
  },
  methods: {
    sendEmail(email) {
      document.location = `mailto:${email}`;
    },
    call(number) {
      document.location = `tel:${number}`;
    },
  },
};
</script>
<style scoped>
.copylabel {
  cursor: pointer;
  display: inline-block;
  border-bottom: 1px dashed;
}
</style>
