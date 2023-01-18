<template>
  <div class="d-flex flex-column flex-grow-1">
    <v-card>
      <v-row dense class="pa-2 align-center">
        <v-col cols="12" lg="6">
          <div class="display-1">Counts of Bookings</div>
        </v-col>
        <v-col cols="12" lg="6" class="d-flex text-right align-center">
          <v-dialog
            ref="dialog"
            v-model="modal"
            :return-value.sync="date"
            persistent
            width="290px"
          >
            <template v-slot:activator="{ on, attrs }">
              <v-text-field
                v-model="date"
                label="Select a Month"
                prepend-icon="mdi-calendar"
                readonly
                v-bind="attrs"
                v-on="on"
              ></v-text-field>
            </template>
            <v-date-picker v-model="date" type="month" scrollable>
              <v-spacer></v-spacer>
              <v-btn text color="primary" @click="modal = false">
                Cancel
              </v-btn>
              <v-btn text color="primary" @click="save"> OK </v-btn>
            </v-date-picker>
          </v-dialog>
        </v-col>
      </v-row>
      <v-container>
        <div v-if="showChart">
          <apexchart
            type="bar"
            height="350"
            :options="chartOptions"
            :series="series"
          ></apexchart>
        </div>
      </v-container>
    </v-card>
  </div>
</template>

<script>
import { data } from "../../database";
export default {
  data() {
    return {
      number_of_days: 30,
      bookings: [
        0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,
        0, 0, 0, 0, 0, 0,
      ],
      date: "2015-12",
      modal: false,
      showChart: false,
      data,
    };
  },
  computed: {
    series() {
      return [
        {
          data: this.bookings,
        },
      ];
    },

    chartOptions() {
      let categories = [];
      for (var i = 0; i < this.number_of_days; i++) categories.push(`${i + 1}`);
      return {
        chart: {
          type: "bar",
          height: 350,
        },
        plotOptions: {
          bar: {
            horizontal: false,
            columnWidth: "75%",
            endingShape: "rounded",
          },
        },
        dataLabels: {
          enabled: false,
        },
        stroke: {
          show: true,
          width: 2,
          colors: ["transparent"],
        },
        xaxis: {
          categories: categories,
        },
        fill: {
          opacity: 1,
        },
        tooltip: {
          y: {
            formatter: function (val) {
              return val + " bookings";
            },
          },
        },
      };
    },
  },
  mounted() {
    this.showChart = true;
    this.save()
  },
  methods: {
    save() {
      this.bookings = [];
      this.$refs.dialog.save(this.date);
      const partsOfDateSelected = this.date.split("-");
      const yearOfDateSelected = partsOfDateSelected[0];
      const monthOfDateSelected = partsOfDateSelected[1];
      this.number_of_days = new Date(
        yearOfDateSelected,
        monthOfDateSelected,
        0
      ).getDate();
      for (var i = 0; i < this.number_of_days; i++) this.bookings.push(0);
      for (let index = 0; index < this.data.length; index++) {
        let parts = this.data[index].reservation_status_date.split("-");
        if (parts[0] == yearOfDateSelected && parts[1] == monthOfDateSelected)
          this.bookings[parts[2]]++;
      }
    },
  },
};
</script>
