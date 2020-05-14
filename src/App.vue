<template>
  <div id="app">
    <LegendColumn />
    <div class="columnsWrapper">
      <Column
        v-for="(weather, index) in weatherData"
        :key="index"
        :day="weather.day"
        :showDayName="showDayName(index)"
        :hour="weather.hour"
        :forecast_icon="weather.forecast_icon"
        :temperature="weather.temperature"
        :rain="weather.rain"
        :wind_direction="weather.wind_direction"
        :wind_speed="weather.wind_speed"
        :preasure="weather.preasure"
        :height="fillHeight(index)"
        :rotate="windDirectionRotate(index)"
        :tempCircleBottom="tempCircleBottom(index)"
        :tempDescriptionBottom="tempDescriptionBottom(index)"
        :preasureCircleBottom="preasureCircleBottom(index)"
        :preasureDescriptionBottom="preasureDescriptionBottom(index)"
        :preasureLineRotate="preasureLineRotate"
        :preasureLineLength="preasureLineLength"
        :tempLineRotate="tempLineRotate(index)"
        :tempLineLength="tempLineLength(index)"
      />
    </div>
  </div>
</template>

<script>
import Column from "./components/Column";
import LegendColumn from "./components/LegendColumn";
import { weatherData } from "../src/assets/weatherData";

export default {
  name: "App",
  components: {
    Column,
    LegendColumn
  },
  data() {
    return {
      weatherData,
      // day: "Dzisiaj",
      // hour: "00:00",
      // forecast_icon: require("../src/assets/cloud.png"),
      // temperature: "7",
      // rain: "0,2",
      // wind_direction: "Południowy",
      // wind_speed: {
      //   description: "Słaby",
      //   number: "4"
      // },
      // preasure: "1014",
      showDay: false
    };
  },
  methods: {
    showDayName(index) {
      const datas = this.$data.weatherData;

      return datas[index].hour === "00:00" ? true : false;
    },
    fillHeight(index) {
      const datas = this.$data.weatherData;
      let fillHeight =
        parseFloat(datas[index].rain.replace(",", ".").replace(" ", "")) * 20;
      return fillHeight;
    },
    tempCircleBottom(index) {
      // dodać warunek tak aby nie wychodziło poza kontener
      const datas = this.$data.weatherData;
      let tempCircleBottom = parseFloat(datas[index].temperature) * 10 - 24;
      return tempCircleBottom;
    },
    tempDescriptionBottom(index) {
      const datas = this.$data.weatherData;
      let tempDescriptionBottom = parseFloat(datas[index].temperature) * 10 - 6;
      return tempDescriptionBottom;
    },
    preasureCircleBottom(index) {
      // dodać warunek tak aby nie wychodziło poza kontener
      const datas = this.$data.weatherData;
      let tempCircleBottom =
        (parseFloat(datas[index].preasure) - 1000) * 10 - 80;
      return tempCircleBottom;
    },
    preasureDescriptionBottom(index) {
      const datas = this.$data.weatherData;
      let preasureDescriptionBottom =
        (parseFloat(datas[index].preasure) - 1000) * 10 - 62;
      return preasureDescriptionBottom;
    },
    windDirectionRotate(index) {
      const datas = this.$data.weatherData;
      let direction = datas[index].wind_direction;
      let windDirectionRotate;
      if (direction === "Południowy") {
        windDirectionRotate = 0;
      } else if (direction === "Pd.-Zach.") {
        windDirectionRotate = 45;
      } else if (direction === "Zachodni") {
        windDirectionRotate = 90;
      } else if (direction === "Pn.-Zach.") {
        windDirectionRotate = 135;
      } else if (direction === "Północny") {
        windDirectionRotate = 180;
      } else if (direction === "Pn.-Wsch.") {
        windDirectionRotate = 225;
      } else if (direction === "Wschodni") {
        windDirectionRotate = 270;
      } else if (direction === "Pd.-Wsch.") {
        windDirectionRotate = 315;
      }
      return windDirectionRotate;
    },
    tempLineRotate(index) {
      const datas = this.$data.weatherData;
      let columnWidth = 120;
      let thisBottom = parseFloat(datas[index].temperature) * 10 - 24;
      let nextBottom;
      if (index < datas.length - 1) {
        nextBottom = parseFloat(datas[index + 1].temperature) * 10 - 24;
      } else {
        nextBottom = 0;
      }
      let vertical = nextBottom - thisBottom;
      let tangOfAngle = vertical / columnWidth;
      const tempLineRotate = (-Math.atan(tangOfAngle) * 180) / Math.PI;

      return tempLineRotate;
    },
    tempLineLength(index) {
      const datas = this.$data.weatherData;
      let columnWidth = 120;
      let thisBottom = parseFloat(datas[index].temperature) * 10 - 24;
      let nextBottom;
      if (index < datas.length - 1) {
        nextBottom = parseFloat(datas[index + 1].temperature) * 10 - 24;
      } else {
        nextBottom = 0;
      }
      let vertical = nextBottom - thisBottom;
      const tempLineLength = Math.ceil(
        Math.sqrt(Math.pow(columnWidth, 2) + Math.pow(vertical, 2))
      );

      return tempLineLength;
    }
  },
  computed: {
    // tempCircleBottom() {
    //   // dodać warunek tak aby nie wychodziło poza kontener
    //   let tempCircleBottom = parseFloat(this.weatherData[0].temperature) * 10 - 24;
    //   return tempCircleBottom;
    // },

    preasureLineRotate() {
      let horizontal = 120;
      let vertical = 20;
      let tangOfAngle = vertical / horizontal;
      const preasureLineRotate = (-Math.atan(tangOfAngle) * 180) / Math.PI;

      return preasureLineRotate;
    },
    preasureLineLength() {
      let horizontal = 120;
      let vertical = 20;
      const preasureLineLength = Math.ceil(
        Math.sqrt(Math.pow(horizontal, 2) + Math.pow(vertical, 2))
      );

      return preasureLineLength;
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
    display: flex;
    flex-wrap: nowrap;
    overflow: hidden;
  }
}
</style>
