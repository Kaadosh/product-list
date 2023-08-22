<template>
  <li :class="{ 'crossed-out': product.crossedOut }" class="product-item">
    <span @click="crossOut">{{ product.name }}</span>
    <button @click="removeProduct" class="remove-button">Удалить</button>
  </li>
</template>

<script>
export default {
  props: ["product"],
  methods: {
    crossOut() {
      this.$emit("crossOut");
    },
    removeProduct() {
      this.$emit("removeProduct");
    },
  },
};
</script>

<style>
.product-item {
  display: flex;
  align-items: center;
  justify-content: space-between;
  background-color: white;
  padding: 10px;
  margin-bottom: 10px;
  border: 1px solid #e1e1e1;
  border-radius: 3px;
  transition: background-color 0.3s;
  cursor: pointer;
}

.product-item:hover {
  background-color: #f5f5f5;
}

.remove-button {
  padding: 5px 10px;
  background-color: #dc3545;
  color: white;
  border: none;
  border-radius: 3px;
  cursor: pointer;
  transition: background-color 0.3s;
}

.remove-button:hover {
  background-color: #b02a37;
}
</style>
