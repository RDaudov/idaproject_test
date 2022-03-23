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
      transition: all .1s ease 0s;
    }
    &::before,
    &::after {
      content: "";
      background-color: #9e9e9e;
      position: absolute;
      width: 100%;
      height: 3px;
      left: 0;
      transition: all .3s ease 0s;
    }
    &::before {
      top: 0;
    }
    &::after {
      bottom: 1px;
    }
    &.active {
      &::before {
        transform: rotate(45deg);
        top: 14px;
      }
      &::after {
        transform: rotate(-45deg);
        bottom: 12px;
      }
      span {
        opacity: 0;
      }
    }
  }
}
</style>