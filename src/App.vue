<template>
  <div id="app">
    <Column
      day="Dzień"
      hour="Godzina"
      forecast="Prognoza"
      temperature="Temperatura"
      rain="Opady"
      wind_direction="Kierunek wiatru"
      wind_speed="Prędkość wiatru"
      preasure="Ciśnienie"
    />
  </div>
</template>

<script>
import Column from "./components/Column.vue";

export default {
  name: "App",
  components: {
    Column
  }
};
</script>

<style lang="scss">
#app {
  font-family: Arial, Helvetica, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  margin-top: 60px;
  margin: 0;
  padding: 0;
}
</style>
