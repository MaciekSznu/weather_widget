<template>
  <div id="app">
    <LegendColumn />
    <div class="columnsWrapper">
      <Column
        v-for="weather in weatherData"
        :key="weather.index"
        :day="weather.day"
        :showDayName="showDayName"
        :hour="weather.hour"
        :forecast_icon="weather.forecast_icon"
        :temperature="weather.temperature"
        :rain="weather.rain"
        :wind_direction="weather.wind_direction"
        :wind_speed="weather.wind_speed"
        :preasure="weather.preasure"
        :height="fillHeight"
        :rotate="windDirectionRotate"
        :tempCircleBottom="tempCircleBottom"
        :tempDescriptionBottom="tempDescriptionBottom"
        :preasureCircleBottom="preasureCircleBottom"
        :preasureDescriptionBottom="preasureDescriptionBottom"
        :preasureLineRotate="preasureLineRotate"
        :preasureLineLength="preasureLineLength"
        :tempLineRotate="tempLineRotate"
        :tempLineLength="tempLineLength"
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
  computed: {
    showDayName() {
      return this.hour === "00:00" ? true : false;
    },
    fillHeight() {
      console.log(this);
      let fillHeight =
        parseFloat(this.weatherData[0].rain.replace(",", ".").replace(" ", "")) * 20;
      return fillHeight;
    },
    tempCircleBottom() {
      // dodać warunek tak aby nie wychodziło poza kontener
      let tempCircleBottom = parseFloat(this.weatherData[0].temperature) * 10 - 24;
      return tempCircleBottom;
    },
    tempDescriptionBottom() {
      let tempDescriptionBottom = this.tempCircleBottom + 18;
      return tempDescriptionBottom;
    },
    tempLineRotate() {
      let horizontal = 120;
      let vertical = 20;
      let tangOfAngle = vertical / horizontal;
      const tempLineRotate = (-Math.atan(tangOfAngle) * 180) / Math.PI;

      return tempLineRotate;
    },
    tempLineLength() {
      let horizontal = 120;
      let vertical = 20;
      const tempLineLength = Math.ceil(
        Math.sqrt(Math.pow(horizontal, 2) + Math.pow(vertical, 2))
      );

      return tempLineLength;
    },
    preasureCircleBottom() {
      // dodać warunek tak aby nie wychodziło poza kontener
      let tempCircleBottom = (parseFloat(this.weatherData[0].preasure) - 1000) * 10 - 80;
      return tempCircleBottom;
    },
    preasureDescriptionBottom() {
      let preasureDescriptionBottom = this.preasureCircleBottom + 18;
      return preasureDescriptionBottom;
    },
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
    },
    windDirectionRotate() {
      let direction = this.weatherData[0].wind_direction;
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
