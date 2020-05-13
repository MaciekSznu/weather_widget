<template>
  <div id="app">
    <LegendColumn />
    <div class="columnsWrapper">
      <Column
        :day="day"
        :showDayName="showDayName"
        :hour="hour"
        :forecast_icon="forecast_icon"
        :temperature="temperature"
        :rain="rain"
        :wind_direction="wind_direction"
        :wind_speed="wind_speed"
        :preasure="preasure"
        :height="fillHeight"
        :rotate="windDirectionRotate"
        :tempCircleBottom="tempCircleBottom"
        :tempDescriptionBottom="tempDescriptionBottom"
        :preasureCircleBottom="preasureCircleBottom"
        :preasureDescriptionBottom="preasureDescriptionBottom"
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
      hour: "00:00",
      forecast_icon: require("../src/assets/cloud.png"),
      temperature: "7",
      rain: "0,2",
      wind_direction: "Południowy",
      wind_speed: {
        description: "Słaby",
        number: "4"
      },
      preasure: "1014",
      showDay: false
    };
  },
  computed: {
    showDayName() {
      return this.hour === "00:00" ? true : false;
    },
    fillHeight() {
      let fillHeight =
        parseFloat(this.rain.replace(",", ".").replace(" ", "")) * 20;
      return fillHeight;
    },
    tempCircleBottom() {
      // dodać warunek tak aby nie wychodziło poza kontener
      let tempCircleBottom = parseFloat(this.temperature) * 10 - 24;
      return tempCircleBottom;
    },
    tempDescriptionBottom() {
      let tempDescriptionBottom = this.tempCircleBottom + 18;
      return tempDescriptionBottom;
    },
    preasureCircleBottom() {
      // dodać warunek tak aby nie wychodziło poza kontener
      let tempCircleBottom = (parseFloat(this.preasure) - 1000) * 10 - 80;
      return tempCircleBottom;
    },
    preasureDescriptionBottom() {
      let preasureDescriptionBottom = this.preasureCircleBottom + 18;
      return preasureDescriptionBottom;
    },
    windDirectionRotate() {
      let direction = this.wind_direction;
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
