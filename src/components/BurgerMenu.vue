<template>
  <button class="burger">
    <span></span>
  </button>
</template>

<script>
export default {
  name: "BurgerMenu",
};
</script>

<style lang="scss" scoped>
.burger {
  display: none;
}
@media only screen and (max-width: 768px) {
  .burger {
    display: block;
    position: relative;
    width: 40px;
    height: 30px;
    margin-top: 3px;
    border: none;
    background-color: transparent;
    span {
      position: absolute;
      background-color: #9e9e9e;
      width: 100%;
      height: 3px;
      top: 13px;
      left: 0;
    }
    &::before,
    &::after {
      content: "";
      background-color: #9e9e9e;
      position: absolute;
      width: 100%;
      height: 3px;
      left: 0;
    }
    &::before {
      top: 0;
    }
    &::after {
      bottom: 1px;
    }
  }
}
</style>