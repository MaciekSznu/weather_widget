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
        :preasureLineRotate="preasureLineRotate(index)"
        :preasureLineLength="preasureLineLength(index)"
        :tempLineRotate="tempLineRotate(index)"
        :tempLineLength="tempLineLength(index)"
        :isFirst="isFirst(index)"
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
      showDay: false,
      columnWidth: 120
    };
  },
  methods: {
    datas() {
      let datas = this.$data.weatherData;
      return datas;
    },
    showDayName(index) {
      return this.datas()[index].hour === "00:00" ? true : false;
    },
    isFirst(index) {
      let isFirst;
      if (index === 0) {
        isFirst = "block";
      }
      return isFirst;
    },
    fillHeight(index) {
      let fillHeight =
        parseFloat(
          this.datas()
            [index].rain.replace(",", ".")
            .replace(" ", "")
        ) * 20;
      return fillHeight;
    },
    tempCircleBottom(index) {
      // dodać warunek tak aby nie wychodziło poza kontener
      let tempCircleBottom =
        parseFloat(this.datas()[index].temperature) * 10 - 24;
      return tempCircleBottom;
    },
    tempDescriptionBottom(index) {
      let tempDescriptionBottom =
        parseFloat(this.datas()[index].temperature) * 10 - 6;
      return tempDescriptionBottom;
    },
    preasureCircleBottom(index) {
      // dodać warunek tak aby nie wychodziło poza kontener
      let tempCircleBottom =
        (parseFloat(this.datas()[index].preasure) - 1000) * 10 - 80;
      return tempCircleBottom;
    },
    preasureDescriptionBottom(index) {
      let preasureDescriptionBottom =
        (parseFloat(this.datas()[index].preasure) - 1000) * 10 - 62;
      return preasureDescriptionBottom;
    },
    windDirectionRotate(index) {
      let direction = this.datas()[index].wind_direction;
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
    tempVertical(index) {
      let thisBottom = parseFloat(this.datas()[index].temperature) * 10 - 24;
      let nextBottom;
      if (index < this.datas().length - 1) {
        nextBottom = parseFloat(this.datas()[index + 1].temperature) * 10 - 24;
      } else {
        nextBottom = thisBottom;
      }
      let tempVertical = nextBottom - thisBottom;

      return tempVertical;
    },
    tempLineRotate(index) {
      let tangOfAngle = this.tempVertical(index) / this.columnWidth;
      const tempLineRotate = (-Math.atan(tangOfAngle) * 180) / Math.PI;

      return tempLineRotate;
    },
    tempLineLength(index) {
      let tempLineLength;
      if (index === this.datas().length - 1) {
        tempLineLength = this.columnWidth / 2;
      } else {
        tempLineLength = Math.ceil(
          Math.sqrt(
            Math.pow(this.columnWidth, 2) +
              Math.pow(this.tempVertical(index), 2)
          )
        );
      }

      return tempLineLength;
    },
    preasureVertical(index) {
      let thisBottom = parseFloat(this.datas()[index].preasure) * 10 - 24;
      let nextBottom;
      if (index < this.datas().length - 1) {
        nextBottom = parseFloat(this.datas()[index + 1].preasure) * 10 - 24;
      } else {
        nextBottom = thisBottom;
      }
      let preasureVertical = nextBottom - thisBottom;

      return preasureVertical;
    },
    preasureLineRotate(index) {
      let tangOfAngle = this.preasureVertical(index) / this.columnWidth;
      const preasureLineRotate = (-Math.atan(tangOfAngle) * 180) / Math.PI;

      return preasureLineRotate;
    },
    preasureLineLength(index) {
      let preasureLineLength;
      if (index === this.datas().length - 1) {
        preasureLineLength = this.columnWidth / 2;
      } else {
        preasureLineLength = Math.ceil(
          Math.sqrt(
            Math.pow(this.columnWidth, 2) +
              Math.pow(this.preasureVertical(index), 2)
          )
        );
      }

      return preasureLineLength;
    }
  },
  computed: {}
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
    //border: 1px solid grey;
    display: flex;
    flex-wrap: nowrap;
    overflow: hidden;
  }
}
</style>
