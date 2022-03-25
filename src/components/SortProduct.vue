<template>
  <select class="sort" id="sort" v-model="modelValue" @change="changeOption">
    <option selected value="">По умолчанию</option>
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
  data() {
    return {
      modelValue: ''
    }
  },
  props: {
    options: {
      type: Array,
      default: () => []
    }
  },
  methods: {
    changeOption(event) {
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
  margin-right: 15px;
  transition: all 0.3s ease 0s;
  &:focus-visible {
    outline: none;
  }
}
</style>