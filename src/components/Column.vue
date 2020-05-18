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
      <div
        class="column__temperature--first-line"
        :style="{
          bottom: tempCircleBottom + 'px',
          display: isFirst
        }"
      ></div>
    </div>
    <div class="column__rain">
      <p class="column__rain--description" v-if="rain !== '' && rain !== '0'">
        {{ rain }} mm
      </p>
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
      <p class="column__wind-speed--description">
        {{ wind_speed.description }}
      </p>
      <p class="column__wind-speed--value">{{ wind_speed.number }} km/h</p>
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
      <div
        class="column__preasure--first-line"
        :style="{
          bottom: preasureCircleBottom + 'px',
          display: isFirst
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
    preasureLineLength: Number,
    isFirst: String
  }
};
</script>

<style scoped lang="scss">
.column {
  box-sizing: border-box;
  height: 920px;
  width: 120px;
  min-width: 120px;
  color: #000000;
  font-size: 20px;
  font-weight: 400;
  background-color: #ffffff;
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

  &__hour,
  &__forecast,
  &__temperature,
  &__rain,
  &__preasure {
    border-right: 1px solid #e5e5e5;
  }

  &__day {
    height: 30px;
    border-right: none;
    font-size: 24px;
    font-weight: 500;
    text-transform: uppercase;
    color: #7e7e7e;
  }
  &__hour {
    height: 60px;
    font-size: 26px;
    font-weight: 500;
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
    font-size: 34px;
    font-weight: 500;

    &--description {
      margin: 0;
      position: absolute;
    }
    &--circle {
      width: 18px;
      height: 18px;
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
      margin-bottom: 8px;
      transform-origin: center left;
    }
    &--first-line {
      position: absolute;
      height: 2px;
      left: 0px;
      width: 60px;
      background-color: #ffd520;
      margin-bottom: 7px;
      display: none;
    }
  }
  &__rain {
    justify-content: flex-end;
    height: 120px;
    font-size: 22px;
    font-weight: 500;
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
    &--icon {
      height: 56px;
      width: 56px;
    }
    &--description {
      margin-bottom: 0px;
      font-weight: 500;
    }
  }
  &__wind-speed {
    height: 100px;
    border-right: 1px solid #ffffff;
    background-color: #f0f0f0;
    &--description {
      margin: 0;
      font-size: 20px;
      font-weight: 500;
    }
    &--value {
      margin: 0;
      margin-top: 6px;
      font-size: 23px;
      font-weight: 500;
    }
  }
  &__preasure {
    position: relative;
    height: 200px;
    border-bottom: 1px solid #f4f4f4;
    &--description {
      font-size: 21px;
      font-weight: 500;
      margin: 0;
      position: absolute;
    }
    &--circle {
      width: 18px;
      height: 18px;
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
      margin-bottom: 8px;
      transform-origin: center left;
    }
    &--first-line {
      position: absolute;
      height: 2px;
      left: 0px;
      width: 60px;
      background-color: #000000;
      margin-bottom: 7px;
      display: none;
    }
  }
}
</style>
