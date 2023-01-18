<template>
  <div class="d-flex flex-column flex-grow-1">
    <v-card>
      <v-row dense class="pa-2 align-center">
        <v-col cols="12" lg="6">
          <div class="display-1">Statuses of Bookings</div>
        </v-col>
        <v-col cols="12" lg="6" class="d-flex text-right align-center">
          <v-dialog
            ref="dialog"
            v-model="modal"
            :return-value.sync="dates"
            persistent
            width="290px"
          >
            <template v-slot:activator="{ on, attrs }">
              <v-text-field
                v-model="dateRangeText"
                label="Select Date Range"
                prepend-icon="mdi-calendar"
                readonly
                v-bind="attrs"
                v-on="on"
              ></v-text-field>
            </template>
            <v-date-picker v-model="dates" range scrollable>
              <v-spacer></v-spacer>
              <v-btn text color="primary" @click="modal = false">
                Cancel
              </v-btn>
              <v-btn
                text
                color="primary"
                @click="save"
                v-if="dates[0] && dates[1]"
              >
                OK
              </v-btn>
            </v-date-picker>
          </v-dialog>
        </v-col>
      </v-row>
      <div v-if="showChart" align="center">
        <apexchart
          type="donut"
          width="480"
          :options="chartOptions"
          :series="series"
        ></apexchart>
      </div>
    </v-card>
  </div>
</template>

<script>
import { data } from "../../database";
export default {
  data() {
    return {
      dates: ["2014-01-01", "2019-01-01"],
      modal: false,
      showChart: false,
      series: [0, 0, 0, 0],
      chartOptions: {
        plotOptions: {
          pie: {
            donut: {
              size: "0%",
            },
          },
        },

        labels: ["No-Show", "Canceled", "Check-Out", "Check-In"],
        chart: {
          type: "donut",
          width: "2000px",
        },
        responsive: [
          {
            breakpoint: 480,
            options: {
              chart: {
                width: 200,
              },
              legend: {
                position: "bottom",
              },
            },
          },
        ],
      },
      data,
    };
  },
  computed: {
    dateRangeText() {
      return this.dates.join(" ~ ");
    },
  },
  mounted() {
    this.showChart = true;
    this.save();
  },
  methods: {
    save() {
      this.series = [0, 0, 0, 0];
      this.$refs.dialog.save(this.dates);
      let dateFrom = this.dates[0];
      let dateTo = this.dates[1];
      for (let index = 0; index < this.data.length; index++) {
        let dateCheck = this.data[index].reservation_status_date;
        let d1 = dateFrom.split("-");
        let d2 = dateTo.split("-");
        let c = dateCheck.split("-");
        let from = new Date(d1[0], parseInt(d1[1]) - 1, d1[2]);
        let to = new Date(d2[0], parseInt(d2[1]) - 1, d2[2]);
        let check = new Date(c[0], parseInt(c[1]) - 1, c[2]);
        if (check > from && check < to) {
          if (this.data[index].reservation_status == "No-Show")
            this.series[0]++;
          else if (this.data[index].reservation_status == "Canceled")
            this.series[1]++;
          else if (this.data[index].reservation_status == "Check-Out")
            this.series[2]++;
          else if (this.data[index].reservation_status == "Check-In")
            this.series[3]++;
        }
      }
    },
  },
};
</script>
