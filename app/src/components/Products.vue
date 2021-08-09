<template>
  <div class="products">
    <ProductItem
      v-for="product in productsList"
      :key="product.id"
      v-bind:product="product"
      v-on:remove-product-item="removeProduct"
    />
  </div>
</template>

<script>
import ProductItem from "@/components/ProductItem";

export default {
  props: ["productsList"],
  components: {
    ProductItem,
  },
  methods: {
    removeProduct(prodId) {
      this.$emit("remove-product", prodId);
    },
  },
};
</script>

<style lang="scss" scoped>
.products {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  width: 100%;
  max-width: 1028px;
  height: auto;
}
</style>