<template>
  <div class="column">
    <div class="column__day">
      <p v-if="showDayName">{{ day }}</p>
    </div>
    <div class="column__hour">
      <p>{{ hour }}</p>
    </div>
    <div class="column__forecast">
      <img class="column__forecast--icon" :src="forecast_icon" />
    </div>
    <div class="column__temperature">
      <p
        class="column__temperature--description"
        :style="{ bottom: tempDescriptionBottom + 'px' }"
      >
        {{ temperature }}&#176;
      </p>
      <div
        class="column__temperature--circle"
        :style="{ bottom: tempCircleBottom + 'px' }"
      ></div>
      <div
        class="column__temperature--line"
        :style="{
          bottom: tempCircleBottom + 'px',
          transform: 'rotate(' + tempLineRotate + 'deg)',
          width: tempLineLength + 'px'
        }"
      ></div>
    </div>
    <div class="column__rain">
      <p class="column__rain--description">{{ rain }} mm</p>
      <div class="column__rain--fill" :style="{ height: height + 'px' }"></div>
    </div>
    <div class="column__wind-direction">
      <img
        class="column__wind-direction--icon"
        src="../assets/wind_ico.png"
        :style="{ transform: 'rotate(' + rotate + 'deg)' }"
      />
      <p class="column__wind-direction--description">{{ wind_direction }}</p>
    </div>
    <div class="column__wind-speed">
      <p>{{ wind_speed.description }}<br />{{ wind_speed.number }} km/h</p>
    </div>
    <div class="column__preasure">
      <p
        class="column__preasure--description"
        :style="{ bottom: preasureDescriptionBottom + 'px' }"
      >
        {{ preasure }} hPa
      </p>
      <div
        class="column__preasure--circle"
        :style="{ bottom: preasureCircleBottom + 'px' }"
      ></div>
      <div
        class="column__preasure--line"
        :style="{
          bottom: preasureCircleBottom + 'px',
          transform: 'rotate(' + preasureLineRotate + 'deg)',
          width: preasureLineLength + 'px'
        }"
      ></div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Column",
  props: {
    day: String,
    showDayName: Boolean,
    hour: String,
    forecast_icon: String,
    temperature: String,
    tempDescriptionBottom: Number,
    tempCircleBottom: Number,
    tempLineRotate: Number,
    tempLineLength: Number,
    rain: String,
    height: Number,
    wind_direction: String,
    rotate: Number,
    wind_speed: Object,
    preasure: String,
    preasureDescriptionBottom: Number,
    preasureCircleBottom: Number,
    preasureLineRotate: Number,
    preasureLineLength: Number
  }
};
</script>

<style scoped lang="scss">
.column {
  height: 920px;
  width: 120px;
  min-width: 120px;
  color: #000000;
  font-size: 14px;
  font-weight: 500;
  background-color: #ffffff;
  border-right: 1px solid #e5e5e5;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  margin: 0;
  padding: 0;
  cursor: pointer;

  &__day,
  &__hour,
  &__forecast,
  &__temperature,
  &__rain,
  &__wind-direction,
  &__wind-speed,
  &__preasure {
    width: 100%;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }

  &__day {
    height: 30px;
    border-right: none;
  }
  &__hour {
    height: 60px;
    font-size: 18px;
  }
  &__forecast {
    height: 70px;
    &--icon {
      width: 62px;
      height: 62px;
    }
  }
  &__temperature {
    position: relative;
    height: 220px;
    font-size: 24px;
    &--description {
      margin: 0;
      position: absolute;
    }
    &--circle {
      width: 16px;
      height: 16px;
      background-color: #ffffff;
      border: 2px solid #000000;
      border-radius: 50%;
      position: absolute;
      z-index: 1;
    }
    &--line {
      position: absolute;
      height: 2px;
      left: 50%;
      background-color: #ffd520;
      margin-bottom: 7px;
      transform-origin: center left;
    }
  }
  &__rain {
    justify-content: flex-end;
    height: 120px;
    font-size: 16px;
    &--description {
      margin-bottom: 2px;
    }
    &--fill {
      width: 100%;
      background-color: #34ccff;
    }
  }
  &__wind-direction {
    height: 120px;
    border-right: 1px solid #ffffff;
    background-color: #f0f0f0;
    &--description {
      margin-bottom: 2px;
    }
  }
  &__wind-speed {
    height: 100px;
    border-right: 1px solid #ffffff;
    background-color: #f0f0f0;
  }
  &__preasure {
    position: relative;
    height: 200px;
    border-bottom: 1px solid #f4f4f4;
    &--description {
      margin: 0;
      position: absolute;
    }
    &--circle {
      width: 16px;
      height: 16px;
      background-color: #ffffff;
      border: 2px solid #000000;
      border-radius: 50%;
      position: absolute;
      z-index: 1;
    }
    &--line {
      position: absolute;
      height: 2px;
      left: 50%;
      background-color: #000000;
      margin-bottom: 7px;
      transform-origin: center left;
    }
  }
}
</style>
