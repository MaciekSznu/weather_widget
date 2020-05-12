<template>
  <div id="app">
    <LegendColumn />
    <div class="columnsWrapper">
      <Column
        :day="day"
        :hour="hour"
        :forecast="forecast"
        :temperature="temperature"
        :rain="rain"
        :wind_direction="wind_direction"
        :wind_speed="wind_speed"
        :preasure="preasure"
        :height="fillHeight"
      />
    </div>
  </div>
</template>

<script>
import Column from "./components/Column";
import LegendColumn from "./components/LegendColumn";

export default {
  name: "App",
  components: {
    Column,
    LegendColumn
  },
  data() {
    return {
      day: "Dzisiaj",
      hour: "01:00",
      forecast: "Prognoza",
      temperature: "7",
      rain: "0,2",
      wind_direction: "Południowy",
      wind_speed: {
        description: "Słaby",
        number: "4"
      },
      preasure: "1014"
    };
  },
  computed: {
    fillHeight() {
      let height = parseFloat(this.rain.replace(",", ".").replace(" ", "")) * 20;
      return height;
    }
  }
};
</script>

<style lang="scss">
#app {
  font-family: Arial, Helvetica, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  box-sizing: border-box;
  text-align: center;
  margin-top: 60px;
  margin: 0;
  padding: 0;
  display: flex;
  height: 920px;

  .columnsWrapper {
    width: 1440px;
    border: 1px solid grey;
  }
}
</style>
