<template>
  <div class="products">
    <transition-group name="list">
      <ProductItem
        v-for="product in productsList"
        :key="product.id"
        v-bind:product="product"
        v-on:remove-product-item="removeProduct"
      />
    </transition-group>
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
.list-enter,
.list-leave-to {
  opacity: 0;
  -webkit-transform: translateY(30px);
  transform: translateY(30px);
}

.list-leave-active {
  position: absolute;
}

.products {
  display: -webkit-box;
  display: flex;
  flex-wrap: wrap;
  -webkit-box-pack: justify;
  justify-content: space-between;
  width: 100%;
  max-width: 1028px;
  height: auto;
}
</style>