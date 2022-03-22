<template>
  <header class="header">
    <h1 class="title">Добавление товара</h1>
    <burger-menu @click="isActive = !isActive" />
    <sort-product v-model="selectedSort" :options="sortOptions" />
  </header>
  <div class="main">
    <form-add @add="addTo" :class="{ active: isActive}" />
    <product-list :products="sortProduct" @remove="removeFrom" />
  </div>
</template>

<script>
import FormAdd from "./components/FormAdd.vue";
import ProductList from "./components/ProductList.vue";
import SortProduct from "./components/SortProduct.vue";
import BurgerMenu from "./components/BurgerMenu.vue";
export default {
  name: "App",
  components: {
    FormAdd,
    ProductList,
    SortProduct,
    BurgerMenu,
  },
  data() {
    return {
      isActive: false,
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
        { value: "priceMin", name: "По цене min" },
        { value: "priceMax", name: "По цене max" },
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
        case "name":
          return [...this.products].sort((a, b) => {
            return a[this.selectedSort]?.localeCompare(b[this.selectedSort]);
          });
        case "priceMin":
          return [...this.products].sort(
            (a, b) => parseFloat(a.price) - parseFloat(b.price)
          );
        case "priceMax":
          return [...this.products].sort(
            (a, b) => parseFloat(b.price) - parseFloat(a.price)
          );
        default:
          return this.products;
      }
    },
  },
};
</script>

<style lang="scss" scoped>
#app {
  background: #e5e5e5;
  max-width: 1440px;
  padding: 0 32px;
  margin: auto;
  padding: 32px;
  display: flex;
  flex-direction: column;
  box-sizing: border-box;
}

.header {
  display: flex;
  justify-content: space-between;
  max-width: 1440px;
  margin: auto;
}

.main {
  display: flex;
  justify-content: flex-start;
  max-width: 1440px;
  margin: auto;
}

.title {
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

@media only screen and (max-width: 768px) {
  .main {
    display: flex;
    flex-direction: column;
  }

  .title {
    display: none;
  }

  .header {
    position: sticky;
    top: 0;
    z-index: 2;
    height: 41px;
    background-color: ghostwhite;
    padding: 8px;
  }

  .product-list {
    padding-top: 15px;
  }
}
</style>
