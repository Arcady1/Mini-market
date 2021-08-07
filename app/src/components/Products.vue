<template>
  <div class="products">
    <ProductItem />
  </div>
</template>

<script>
import ProductItem from "@/components/ProductItem";

export default {
  components: {
    ProductItem,
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