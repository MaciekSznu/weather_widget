<template>
  <div class="column">
    <div class="column__day">
      <p v-if="showDayName">{{ day }}</p>
    </div>
    <div class="column__hour">
      <p>{{ hour }}</p>
    </div>
    <div class="column__forecast">
      <span>{{ forecast }}</span>
    </div>
    <div class="column__temperature">
      <p>{{ temperature }}&#176;</p>
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
      <p>{{ preasure }} hPa</p>
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
    forecast: String,
    temperature: String,
    rain: String,
    height: Number,
    wind_direction: String,
    rotate: Number,
    wind_speed: Object,
    preasure: String
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.column {
  height: 920px;
  width: 120px;
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
  }
  &__temperature {
    height: 220px;
    font-size: 24px;
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
    height: 200px;
    border-bottom: 1px solid #f4f4f4;
  }
}
</style>
