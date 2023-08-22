<template>
  <div class="product-list">
    <h1 class="product-list-title">Список продуктов</h1>
    <div class="product-list-input">
      <input
        class="product-list-input-field"
        v-model="newProduct"
        @keyup.enter="addProduct"
        placeholder="Добавить продукт"
      />
      <button class="product-list-add-button" @click="addProduct">
        Добавить
      </button>
    </div>
    <ul>
      <product-item
        v-for="(product, index) in products"
        :key="product.id"
        :product="product"
        @crossOut="crossOut(index)"
        @removeProduct="removeProduct(index)"
      />
    </ul>
  </div>
</template>

<script>
import ProductItem from "./ProductItem.vue";

export default {
  components: {
    ProductItem,
  },
  data() {
    return {
      products: [],
      newProduct: "",
    };
  },
  methods: {
    addProduct() {
      if (this.newProduct.trim() !== "") {
        this.products.push({
          id: Date.now(),
          name: this.newProduct,
          crossedOut: false,
        });
        this.newProduct = "";
      }
    },
    removeProduct(index) {
      this.products.splice(index, 1);
    },
    crossOut(index) {
      this.products[index].crossedOut = true;
      this.products.push(this.products.splice(index, 1)[0]);
    },
  },
  mounted() {
    const savedProducts = localStorage.getItem("products");
    if (savedProducts) {
      this.products = JSON.parse(savedProducts);
    }
  },
  watch: {
    products: {
      handler() {
        localStorage.setItem("products", JSON.stringify(this.products));
      },
      deep: true,
    },
  },
};
</script>

<style>
.product-list {
  font-family: Arial, sans-serif;
  max-width: 400px;
  margin: 0 auto;
  padding: 20px;
  background-color: #f5f5f5;
  border-radius: 5px;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
}

.product-list-title {
  text-align: center;
  margin-bottom: 20px;
}

.product-list-input {
  display: flex;
  align-items: center;
  margin-bottom: 15px;
}

.product-list-input-field {
  flex: 1;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 3px;
  font-size: 14px;
}

.product-list-add-button {
  padding: 10px 15px;
  background-color: #007bff;
  color: white;
  border: none;
  border-radius: 3px;
  cursor: pointer;
  transition: background-color 0.3s;
}

.product-list-add-button:hover {
  background-color: #0056b3;
}

.crossed-out {
  text-decoration: line-through;
  color: #999;
}
</style>
