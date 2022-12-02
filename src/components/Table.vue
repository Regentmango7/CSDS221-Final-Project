<template>
  <Bar
    :chart-options="chartOptions"
    :chart-data="chartData"
    :chart-id="chartId"
    :dataset-id-key="datasetIdKey"
    :plugins="plugins"
    :css-classes="cssClasses"
    :styles="styles"
    :width="width"
    :height="height"
  />
</template>

<script>
import { Bar } from 'vue-chartjs';
import {
  Chart as ChartJS,
  Title,
  Tooltip,
  Legend,
  BarElement,
  CategoryScale,
  LinearScale,
  Plugin,
} from 'chart.js';
import axios from 'axios';

export default {
  name: 'Table',
  components: { Bar },
  data: {
    pokeData: {
      type: Array,
      default: [],
    },
  },
  props: {
    chartId: {
      type: String,
      default: 'bar-chart',
    },
    datasetIdKey: {
      type: String,
      default: 'label',
    },
    width: {
      type: Number,
      default: 400,
    },
    height: {
      type: Number,
      default: 400,
    },
    cssClasses: {
      default: '',
      type: String,
    },
    styles: {
      type: Object,
      default: () => {},
    },
    plugins: {
      type: Object,
      default: () => {},
    },
  },
  methods: {
    getLabels() {
      let label = [];
      this.pokeData.forEach((el) => {
        label.append(el.name);
      });
      this.chartData.labels = label;
    },
    getCounts() {
      let count = [];
      this.pokeData.forEach((el) => {
        count.append(el.count);
      });
      this.chartData.datasets[0].data = count;
    },
    loadingFinished() {
      console.timeEnd('data');
    },
    typeLoadingFinished() {
      console.timeEnd('types');
    },
  },
  data() {
    return {
      chartData: {
        labels: ['Hello'],
        datasets: [
          {
            label: '# of Pokemon',
            data: [10],
            backgroundColor: ['rgba(54, 162, 235, 0.7)'],
            borderColor: ['rgba(54, 162, 235, 1)'],
            borderWidth: 2,
          },
        ],
      },
      chartOptions: {
        responsive: true,
      },
      dataLoaded: false,
      typesLoaded: false,
    };
  },
  watch: {
    dataLoaded() {
      this.dataLoaded && this.loadingFinished();
    },
    typesLoaded() {
      this.typesLoaded && this.typeLoadingFinished();
    },
  },
  created() {
    console.time('data');
    axios
      .get('https://pokeapi.co/api/v2/type/')
      .then((res) => {
        this.pokeData = res.data.results;
      })
      .finally(() => {
        this.dataLoaded = true;
        console.time('types');
        this.pokeData.forEach((el, index) => {
          axios
            .get(el.url)
            .then((res) => {
              el['count'] = res.data.pokemon.length;
            })
            .finally(() => {
              if (index == this.pokeData.length - 1) {
                this.typesLoaded = true;
                console.log('data', this.pokeData);
              }
            });
        });
      });
  },
  mounted() {
    //alert();
    //this.getCounts();
    //this.getLabels();
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
