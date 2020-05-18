<template>
  <div class="button-column">
    <div class="button-column__button">
      <div
        class="button-column__button--icon"
      ></div>
    </div>
  </div>
</template>

<script>
export default {
  name: "ButtonLeft"
};
</script>

<style scoped lang="scss">
.button-column {
  height: 100%;
  width: 120px;
  min-width: 120px;
  background: linear-gradient(
    90deg,
    rgba(215, 215, 215, 1) 0%,
    rgba(255, 255, 255, 0) 15%,
    rgba(255, 255, 255, 0) 100%
  );
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: flex-start;
  margin: 0;
  padding: 0;
  cursor: pointer;

  &__button {
    background-color: #e5e5e5;
    height: 120px;
    width: 60px;
    border-top-right-radius: 60px;
    border-bottom-right-radius: 60px;
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
      border-right: 24px solid #ffffff;
      border-bottom: 12px solid transparent;
    }
  }
}
</style>
