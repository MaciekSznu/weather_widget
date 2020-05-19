<template>
  <div class="panel">
    <div class="panel__button" @click="slideRight()">
      <div class="panel__button--icon"></div>
    </div>
  </div>
</template>

<script>
export default {
  name: "RightPanel",
  methods: {
    slideRight() {
      this.$root.$emit("slide-right");
    }
  }
};
</script>

<style scoped lang="scss">
.panel {
  height: 100%;
  width: 120px;
  min-width: 120px;
  background: linear-gradient(
    90deg,
    rgba(255, 255, 255, 0) 0%,
    rgba(255, 255, 255, 1) 100%
  );
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: flex-end;
  margin: 0;
  padding: 0;
  cursor: pointer;

  &__button {
    background-color: #e5e5e5;
    height: 120px;
    width: 60px;
    border-top-left-radius: 60px;
    border-bottom-left-radius: 60px;
    display: flex;
    justify-content: center;
    align-items: center;
    opacity: 0.6;

    &:hover {
      opacity: 0.85;
    }

    &--icon {
      width: 0;
      height: 0;
      border-top: 12px solid transparent;
      border-left: 24px solid #ffffff;
      border-bottom: 12px solid transparent;
    }
  }
}
</style>
