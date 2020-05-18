<template>
  <div class="column">
    <div class="column__day">
      <p>Dzień</p>
    </div>
    <div class="column__hour">
      <p>Godzina</p>
    </div>
    <div class="column__forecast">
      <p>Prognoza</p>
    </div>
    <div class="column__temperature">
      <p>Temperatura</p>
    </div>
    <div class="column__rain">
      <p></p>
      Opady
    </div>
    <div class="column__wind-direction">
      <p>Kierunek wiatru</p>
    </div>
    <div class="column__wind-speed">
      <p>Prędkość wiatru</p>
    </div>
    <div class="column__preasure">
      <p>Ciśnienie</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "Legend_Column"
};
</script>

<style scoped lang="scss">
.column {
  height: 920px;
  width: 140px;
  min-width: 140px;
  color: #7e7e7e;
  font-size: 20px;
  font-weight: 400;
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
    border-bottom: 2px solid #f4f4f4;
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
  }

  &__forecast {
    height: 70px;
  }

  &__temperature {
    height: 220px;
  }

  &__rain {
    height: 120px;
  }

  &__wind-direction {
    height: 120px;
  }

  &__wind-speed {
    height: 100px;
  }

  &__preasure {
    height: 200px;
    border-bottom: none;
  }
}
</style>
