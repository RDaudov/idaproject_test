<template>
  <form class="form">
    <label for="name" class="label">Наименование товара<span></span></label>
    <input
      class="input"
      @input="product.name = $event.target.value"
      :class="{ invalid: v$.name.$error }"
      type="text"
      placeholder="Введите наименование товара"
      v-model="v$.name.$model"
    />
    <small class="error" v-if="v$.name.$error"
      >Поле является обязательным
    </small>
    <label for="description" class="label">Описание товара</label>
    <textarea
      class="input description"
      @input="product.description = $event.target.value"
      type="text"
      placeholder="Введите описание товара"
      v-model="v$.description.$model"
    ></textarea>
    <label for="link" class="label"
      >Ссылка на изображение товара<span></span
    ></label>
    <input
      class="input"
      @input="product.link = $event.target.value"
      :class="{ invalid: v$.link.$error }"
      type="text"
      v-model="v$.link.$model"
      placeholder="Введите ссылку"
    />
    <small class="error" v-if="v$.link.$error"
      >Поле является обязательным</small
    >
    <label for="price" class="label">Цена товара<span></span></label>
    <input
      class="input"
      @input="product.price = $event.target.value"
      v-imask="mask"
      :class="{ invalid: v$.price.$error }"
      type="text"
      v-model.number="v$.price.$model"
      placeholder="Введите цену"
    />
    <small class="error" v-if="v$.price.$error"
      >Поле является обязательным</small
    >
    <button
      class="button"
      type="submit"
      :disabled="v$.$error"
      @click="submit"
      @click.prevent="addTo"
      :class="{ active: !v$.$invalid }"
    >
      Добавить товар
    </button>
  </form>
</template>

<script>
import useVuelidate from "@vuelidate/core";
import { required } from "@vuelidate/validators";
import { IMaskDirective } from "vue-imask";

export default {
  name: "FormAdd",
  emits: ["add"],
  props: {
    products: {
      type: Array,
    },
  },
  setup() {
    return { v$: useVuelidate() };
  },
  data() {
    return {
      product: {
        name: "",
        description: "",
        link: "",
        price: "",
      },
      mask: {
        mask: "000000000000000",
        lazy: true,
      },
      description: "",
      name: "",
      link: "",
      price: "",
    };
  },
  validations() {
    return {
      name: { required },
      link: { required },
      price: { required },
      description: "",
    };
  },
  methods: {
    async submit() {
      const isFormCorrect = await this.v$.$validate();
      if (!isFormCorrect) return;
    },
    addTo() {
      if (this.name && this.link && this.price) {
        this.$emit("add", this.product);
        this.product = {
          name: "",
          description: "",
          link: "",
          price: "",
        };
      }
    },
  },
  directives: {
    imask: IMaskDirective,
  },
};
</script>

<style lang="scss" scoped>
.form {
  font-family: Source Sans Pro, sans-serif;
  font-style: normal;
  font-weight: normal;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  width: 332px;
  height: 440px;
  box-sizing: border-box;
  padding: 24px;
  background: #fffefb;
  box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04),
    0px 6px 10px rgba(0, 0, 0, 0.02);
  border-radius: 4px;
  margin: 24px 8px;
  position: sticky;
  top: 24px;
}

.input {
  height: 36px;
  width: 100%;
  background: #fffefb;
  box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
  border-radius: 4px;
  border: none;
  resize: none;
  box-sizing: border-box;
  margin-bottom: 16px;
  padding-left: 16px;
  &.invalid {
    border: 1px solid #ff8484;
    margin-bottom: unset;
  }
  &::placeholder {
    font-family: Source Sans Pro;
    font-style: normal;
    font-weight: normal;
    font-size: 12px;
    line-height: 15px;
    color: #b4b4b4;
  }
  &:focus-visible {
    border: 1px #0480a1d1 solid;
    outline: none;
  }
  &:hover {
    box-shadow: 0px 4px 4px rgb(0 0 0 / 20%);
    border-bottom: 1px #0480a1d1 solid;
  }
}
.description {
  height: 108px;
  padding-top: 10px;
}

.error {
  font-size: 8px;
  line-height: 10px;
  letter-spacing: -0.02em;
  color: #ff8484;
  align-self: baseline;
  margin: 4px 0 2px;
}

.label {
  align-self: flex-start;
  font-size: 10px;
  line-height: 13px;
  letter-spacing: -0.02em;
  color: #49485e;
  padding-bottom: 4px;
  span {
    display: inline-block;
    background: #ff8484;
    border-radius: 4px;
    width: 4px;
    height: 4px;
    vertical-align: top;
  }
}

.button {
  font-family: Inter;
  font-style: normal;
  font-weight: 600;
  font-size: 12px;
  line-height: 15px;
  text-align: center;
  letter-spacing: -0.02em;
  color: #b4b4b4;
  background: #eeeeee;
  border-radius: 10px;
  height: 36px;
  width: 284px;
  border: none;
  margin-top: 10px;
  &.active {
    color: #ffffff;
    background: #7bae73;
    box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.1);
    &:hover {
      box-shadow: 0px 4px 6px rgb(0 0 0 / 35%);
    }
  }
}

@media only screen and (max-width: 740px) {
  .form {
    position: unset;
  }
}
</style>