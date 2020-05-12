<template>
  <div class="column">
    <div class="column__day">
      <p>{{ day }}</p>
    </div>
    <div class="column__hour">
      <p>{{ hour }}</p>
    </div>
    <div class="column__forecast">
      <p>{{ forecast }}</p>
    </div>
    <div class="column__temperature">
      <p>{{ temperature }}</p>
    </div>
    <div class="column__rain">
      <p></p>
      {{ rain }}
    </div>
    <div class="column__wind-direction">
      <p>{{ wind_direction }}</p>
    </div>
    <div class="column__wind-speed">
      <p>{{ wind_speed }}</p>
    </div>
    <div class="column__preasure">
      <p>{{ preasure }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "Column",
  props: {
    day: String,
    hour: String,
    forecast: String || Object,
    temperature: String,
    rain: String,
    wind_direction: String,
    wind_speed: String,
    preasure: String
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.column {
  height: 920px;
  width: 120px;
  color: #b3b3b3;
  font-size: 14px;
  font-weight: 600;
  background-color: #ffffff;
  //border-bottom: 1px solid #f4f4f4;
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
    border-bottom: 1px solid #f4f4f4;
    width: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
  }

  &__day {
    height: 30px;
    border-right: none;
  }
  &__hour {
    height: 60px;
    //font-size: 18px;
  }
  &__forecast {
    height: 70px;
  }
  &__temperature {
    height: 220px;
    //font-size: 24px;
  }
  &__rain {
    height: 120px;
    //font-size: 16px;
  }
  &__wind-direction {
    height: 120px;
    border-right: 1px solid #ffffff;
    background-color: #f0f0f0;
  }
  &__wind-speed {
    height: 100px;
    border-right: 1px solid #ffffff;
    background-color: #f0f0f0;
  }
  &__preasure {
    height: 200px;
    border-bottom: none;
  }
}
</style>
