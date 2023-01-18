<template>
  <div class="d-flex flex-column flex-grow-1">
    <v-card>
      <v-row dense class="pa-2 align-center">
        <v-col cols="12" lg="6">
          <div class="display-1">Count of Visitors</div>
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
      <div v-if="showChart">
        <apexchart
          type="bar"
          height="350"
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
      dates: ["2016-01-01", "2016-01-04"],
      modal: false,
      categories: [],
      showChart: false,
      series: [
        {
          name: "Adults",
          data: [],
        },
        {
          name: "Children",
          data: [],
        },
        {
          name: "Babies",
          data: [],
        },
      ],
      data,
    };
  },
  computed: {
    dateRangeText() {
      return this.dates.join(" ~ ");
    },
    chartOptions() {
      return {
        chart: {
          type: "bar",
          height: 350,
        },
        plotOptions: {
          bar: {
            horizontal: false,
            columnWidth: "55%",
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
          categories: this.categories,
        },
        yaxis: {
          title: {
            text: "$ (thousands)",
          },
        },
        fill: {
          opacity: 1,
        },
        tooltip: {
          y: {
            formatter: function (val) {
              return val;
            },
          },
        },
      };
    },
  },
  mounted() {
    this.showChart = true;
    this.save();
  },
  methods: {
    generateDateList(from, to) {
      var getDate = function (date) {
        var m = date.getMonth(),
          d = date.getDate();
        return (
          date.getFullYear() +
          "-" +
          (m < 10 ? "0" + m : m) +
          "-" +
          (d < 10 ? "0" + d : d)
        );
      };
      var fs = from.split("-"),
        startDate = new Date(fs[0], fs[1], fs[2]),
        result = [getDate(startDate)],
        start = startDate.getTime(),
        ts,
        end;

      if (typeof to == "undefined") {
        end = new Date().getTime();
      } else {
        ts = to.split("-");
        end = new Date(ts[0], ts[1], ts[2]).getTime();
      }
      while (start < end) {
        start += 86400000;
        startDate.setTime(start);
        result.push(getDate(startDate));
      }
      return result;
    },
    save() {
      this.series = [
        {
          name: "Adults",
          data: [],
        },
        {
          name: "Children",
          data: [],
        },
        {
          name: "Babies",
          data: [],
        },
      ];
      this.categories = [];
      this.$refs.dialog.save(this.dates);
      let dateFrom = this.dates[0];
      let dateTo = this.dates[1];
      this.categories = this.generateDateList(dateFrom, dateTo);
      for (var i = 0; i < this.categories.length; i++) {
        this.series[0].data.push(0);
        this.series[1].data.push(0);
        this.series[2].data.push(0);
      }
      for (let index = 0; index < this.data.length; index++) {
        let dateCheck = this.data[index].reservation_status_date;
        if (this.categories.includes(dateCheck)) {
          this.series[0].data[this.categories.indexOf(dateCheck)] =
            this.series[0].data[this.categories.indexOf(dateCheck)] +
            parseInt(this.data[index].adults);
          this.series[1].data[this.categories.indexOf(dateCheck)] =
            this.series[1].data[this.categories.indexOf(dateCheck)] +
            parseInt(this.data[index].children);
          this.series[2].data[this.categories.indexOf(dateCheck)] =
            this.series[2].data[this.categories.indexOf(dateCheck)] +
            parseInt(this.data[index].babies);
        }
      }
    },
  },
};
</script>
