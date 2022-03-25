<template>
  <div class="product-list">
    <transition-group name="list" key="item">
      <div
        class="product-wrap"
        v-for="product in products"
        :key="product.id"
        @remove="$emit('remove', product)"
      >
        <div class="img-wrap">
          <img class="img" :src="product.link" alt="product" />
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
    </transition-group>
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
.list-enter-active,
.list-leave-active {
  transition: all 2s ease;
}

.list-enter-from,
.list-leave-to {
  opacity: 0;
  scale: 0;
  transform: rotate3d(1, 0, 0, 93deg);
}

.delete {
  display: flex;
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
  transform: scale(0.001);
  transition: all 0.3s ease 0s;
  &:hover {
    box-shadow: 0px 4px 4px rgba(0, 0, 0, 0.5);
    transform: scale(1.03);
  }
}
.product-list {
  box-sizing: border-box;
  width: 100%;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  display: grid;
  grid-gap: 16px;
  overflow: auto;
  padding: 16px 8px;
  scrollbar-width: none;
  overflow: visible;
  &::-webkit-scrollbar {
    width: 0;
  }
}

.product-wrap {
  position: relative;
  display: flex;
  max-width: 420px;
  flex-direction: column;
  background: #fffefb;
  box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04),
    1px 6px 10px rgba(0, 0, 0, 0.03);
  border-radius: 4px;
  transition: all 0.5s ease 0s;
  &:hover {
    box-shadow: -1px 7px 8px rgb(0 0 0 / 10%), 10px 10px 10px rgb(0 0 0 / 20%);
    .img {
      transition: all 0.3s ease-in-out 0s;
      transform: scale(1.03);
    }
    .delete {
      transition: all 0.5s ease 0s;
      transform: scale(1);
    }
  }
}

.img-wrap {
  min-height: 200px;
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

@media only screen and (max-width: 1066px) {
  .product-list {
    justify-items: center;
  }
}
</style>