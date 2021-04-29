<template>
  <v-container>
    <v-row justify="center">
      <h1>Analysis</h1>
    </v-row>
    <v-row justify="center">
      <p class="text-center">This is an alpha version of our analysis.</p>
    </v-row>
    <v-row justify="center">
      <div class="chart">
        <PieChart
          v-if="loaded"
          :data="genderChartData"
          :options="genderChartOptions"
        />
      </div>
      <div class="chart">
        <BarChart
          v-if="loaded"
          :data="ageChartData"
          :options="ageChartOptions"
        />
      </div>
    </v-row>
    <v-row justify="center">
      <div class="chart">
        <PieChart
          v-if="loaded"
          :data="deviceChartData"
          :options="deviceChartOptions"
        />
      </div>
      <div class="chart">
        <LineChart
          v-if="loaded"
          :data="weightChartData"
          :options="weightChartOptions"
        />
      </div>
    </v-row>
  </v-container>
</template>

<script>
import PieChart from '~/components/charts/PieChart.vue'
import BarChart from '~/components/charts/BarChart.vue'
import LineChart from '~/components/charts/LineChart.vue'
export default {
  components: {
    PieChart,
    BarChart,
    LineChart,
  },
  data() {
    return {
      loaded: false,
      genderChartData: {
        labels: [],
        datasets: [
          {
            data: [],
            backgroundColor: [
              'rgba(255, 99, 132)',
              'rgba(255, 159, 64)',
              'rgba(255, 205, 86)',
            ],
          },
        ],
      },
      genderChartOptions: {
        responsive: true,
        legend: {
          position: 'top',
        },
        title: {
          display: true,
          text: 'Gender',
        },
      },
      ageChartData: {
        labels: [],
        datasets: [
          {
            data: [],
            backgroundColor: [],
          },
        ],
      },
      ageChartOptions: {
        responsive: true,
        legend: {
          display: false,
          position: 'top',
        },
        title: {
          display: true,
          text: 'Ages',
        },
        scales: {
          yAxes: [
            {
              ticks: {
                stepSize: 1,
                beginAtZero: true,
              },
            },
          ],
        },
      },
      deviceChartData: {
        labels: [],
        datasets: [
          {
            data: [],
            backgroundColor: [
              'rgba(255, 99, 132)',
              'rgba(255, 159, 64)',
              'rgba(255, 205, 86)',
              'rgba(75, 192, 192)',
              'rgba(54, 162, 235)',
              'rgba(153, 102, 255)',
            ],
          },
        ],
      },
      deviceChartOptions: {
        responsive: true,
        legend: {
          position: 'top',
        },
        title: {
          display: true,
          text: 'Devices',
        },
      },
      weightChartData: {
        datasets: [
          {
            label: '',
            data: [],
            backgroundColor: [],
          },
        ],
      },
      weightChartOptions: {
        responsive: true,
        legend: {
          position: 'top',
        },
        title: {
          display: true,
          text: 'Weights',
        },
        scales: {
          xAxes: [
            {
              type: 'time',
            },
          ],
        },
      },
    }
  },
  fetch() {
    this.$axios
      .$get('/find-session/' + this.$route.params.session)
      .catch((_) => {
        return this.$nuxt.error({ statusCode: 404 })
      })
  },
  async mounted() {
    this.loaded = false
    try {
      const gender = await this.$axios.$get(
        '/analysis/gender-user/' + this.$route.params.session
      )
      this.genderChartData.labels = gender.labels
      this.genderChartData.datasets[0].data = gender.data
      const age = await this.$axios.$get(
        '/analysis/age-user/' + this.$route.params.session
      )
      this.ageChartData.labels = age.labels
      this.ageChartData.datasets[0].data = age.data
      const device = await this.$axios.$get(
        '/analysis/device-user/' + this.$route.params.session
      )
      this.deviceChartData.labels = device.labels
      this.deviceChartData.datasets[0].data = device.data
      this.ageChartData.datasets[0].data = age.data
      const weight = await this.$axios.$get(
        '/analysis/weight-user/' + this.$route.params.session
      )
      // this.weightChartData.labels = weight[1].label
      // this.weightChartData.datasets[0].data = weight[1].data
      this.weightChartData.datasets = weight
      this.loaded = true
    } catch (e) {}
  },
}
</script>
