<template>
  <h1 class="title">Добавление товара</h1>
  <form-add @add="addTo" />
  <sort-product v-model="selectedSort" :options="sortOptions" />
  <product-list :products="sortProduct" @remove="removeFrom" />
  <input type="button" value="1" @click="sort"/>
</template>

<script>
import FormAdd from "./components/FormAdd.vue";
import ProductList from "./components/ProductList.vue";
import SortProduct from "./components/SortProduct.vue";
export default {
  name: "App",
  components: {
    FormAdd,
    ProductList,
    SortProduct,
  },
  data() {
    return {
      products: [
        {
          id: 1,
          link: "https://i.ibb.co/VS3DyMY/product.png",
          name: "bНаименование товара",
          description:
            "aДовольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание ",
          price: 11000,
        },
        {
          id: 2,
          link: "https://i.ibb.co/VS3DyMY/product.png",
          name: "aНаименование товара",
          description:
            "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание ",
          price: 12000,
        },
        {
          id: 3,
          link: "https://i.ibb.co/VS3DyMY/product.png",
          name: "Наименование товара",
          description:
            "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание ",
          price: 13000,
        },
        {
          id: 4,
          link: "https://i.ibb.co/VS3DyMY/product.png",
          name: "Наименование товара",
          description:
            "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание ",
          price: 10000,
        },
        {
          id: 5,
          link: "https://i.ibb.co/VS3DyMY/product.png",
          name: "Наименование товара",
          description:
            "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание ",
          price: 3000,
        },
        {
          id: 6,
          link: "https://i.ibb.co/VS3DyMY/product.png",
          name: "Наименование товара",
          description:
            "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание ",
          price: 13000,
        },
      ],
      name: "",
      description: "",
      price: "",
      selectedSort: "",
      sortOptions: [
        { value: "name", name: "По наименованию" },
        { value: "priceMin", name: "По цене min" }
      ],
    };
  },
  methods: {
    addTo(product) {
      this.products.push(product);
    },
    removeFrom(product) {
      this.products = this.products.filter((p) => p.id !== product.id);
    },
  },
  computed: {
    sortProduct() {
      switch (this.selectedSort) {
        default:
          return this.products;
        case "name":
          return [...this.products].sort((a, b) => {
            return a[this.selectedSort]?.localeCompare(b[this.selectedSort]);
          });
        case "priceMin":
          return [...this.products].sort((a, b) =>
            a.selectedSort > b.selectedSort ? 1 : -1
          );
      }
    },
  },
};
</script>


<style>
#app {
  background: #e5e5e5;
  margin: auto;
  padding-top: 32px;
  display: grid;
  justify-content: flex-start;
  grid-template-columns: 1fr 7fr;
}

.form {
  grid-area: 2 / 1 / 3 / 2;
}

.product-list {
  grid-area: 2 / 2 / 3 / 3;
}

.title {
  grid-area: 1 / 1 / 2 / 2;
  font-family: Source Sans Pro;
  font-style: normal;
  font-weight: 600;
  font-size: 28px;
  line-height: 35px;
  color: #3f3f3f;
  box-sizing: content-box;
  margin: unset;
  padding-left: 15px;
}

@media only screen and (max-width: 740px) {
  #app {
    display: flex;
    flex-direction: column;
    align-items: center;
  }
}
</style>
