<template>
  <select class="sort" id="sort" v-model="modelValue" @change="changeOption">
    <option disabled value="">По умолчанию</option>
    <option 
    v-for="option in options" 
    :key="option.value" 
    :value="option.value"
    >
      {{ option.name }}
    </option>
  </select>
</template>

<script>
export default {
  name: "SortProduct",
  props: {
    options: {
      type: Array,
      default: () => []
    }
  },
  methods: {
    changeOption(event) {
      console.log(event);
      this.$emit('update:modelValue', event.target.value)
    }
  },
};
</script>

<style lang="scss" scoped>
.sort {
  font-family: Source Sans Pro;
  font-style: normal;
  font-weight: normal;
  font-size: 12px;
  line-height: 15px;
  padding-left: 16px;
  color: #b4b4b4;
  height: 36px;
  background: #fffefb;
  box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
  border-radius: 4px;
  border: none;
  grid-area: 1 / 2 / 2 / 3;
  justify-self: end;
  margin-right: 32px;
  &:focus-visible {
    outline: none;
  }
}
@media only screen and (max-width: 740px) {
  .sort {
    margin-right: unset;
  }
}
</style>