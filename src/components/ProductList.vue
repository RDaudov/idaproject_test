<template>
  <div class="product-list">
    <div
      class="product-wrap"
      v-for="product in products"
      :key="product.id"
      @remove="$emit('remove', product)"
    >
      <div class="img-wrap">
        <img class="img" :srcset="product.link" alt="product" />
      </div>
      <div class="text">
        <div class="name" id="names">{{ product.name }}</div>
        <div class="description" id="descripions">
          {{ product.description }}
        </div>
        <div class="price" id="prices">{{ product.price }}&nbsp;руб.</div>
      </div>
      <div class="delete" @click="$emit('remove', product)">
        <img src="@/assets/delete.svg" />
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: "ProductList",
  emits: ["remove"],
  props: {
    products: {
      type: Object,
    },
  },
  data() {
    return {};
  },
};
</script>
<style lang="scss" scoped>
.delete {
  display: none;
  justify-content: center;
  align-items: center;
  width: 32px;
  height: 32px;
  background-size: contain;
  position: absolute;
  background-color: #ff8484;
  border-radius: 10px;
  box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.1);
  top: -8px;
  right: -8px;
}
.product-list {
  display: flex;
  flex-wrap: wrap;
  max-width: 1044px;
  overflow: auto;
  margin-top: 16px;
  padding: 0 8px;
  scrollbar-width: none;
  &::-webkit-scrollbar {
    width: 0;
  }
}

.product-wrap {
  position: relative;
  width: 332px;
  height: 423px;
  display: flex;
  flex-direction: column;
  background: #fffefb;
  box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04),
    1px 6px 10px rgba(0, 0, 0, 0.03);
  border-radius: 4px;
  margin: 8px;
  &:hover {
    box-shadow: -1px 7px 8px rgb(0 0 0 / 10%), 10px 10px 10px rgb(0 0 0 / 20%);
    .img {
      transform: scale(1.03);
    }
    .delete {
      display: flex;
    }
  }
}

.img-wrap {
  min-height: 200px;
  max-width: 332px;
  margin-bottom: 16px;
  overflow: hidden;
  .img {
    object-fit: cover;
    width: 100%;
    height: 100%;
  }
}

.text {
  word-wrap: break-word;
  min-height: 207px;
  margin: 0 16px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

.name {
  font-family: Source Sans Pro;
  font-style: normal;
  font-weight: 600;
  font-size: 20px;
  line-height: 25px;
  color: #3f3f3f;
  margin-bottom: 16px;
}

.description {
  font-family: Source Sans Pro;
  font-style: normal;
  font-weight: normal;
  font-size: 16px;
  line-height: 20px;
  color: #3f3f3f;
  padding-bottom: 32px;
  overflow: scroll;
  scrollbar-width: none;
  &::-webkit-scrollbar {
    width: 0;
  }
}

.price {
  font-family: Source Sans Pro;
  font-style: normal;
  font-weight: 600;
  font-size: 24px;
  line-height: 30px;
  color: #3f3f3f;
  margin-bottom: 24px;
}

@media only screen and (max-width: 1440px) {
  .product-list {
    justify-content: center;
    max-width: 800px;
    justify-content: flex-end;
  }
}

@media only screen and (max-width: 1120px) {
  .product-list {
    justify-content: center;
    max-width: 400px;
  }
}
</style>