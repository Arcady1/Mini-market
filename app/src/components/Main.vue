<template>
  <main class="main main_margin">
    <Sidebar
      v-bind:sidebarTitles="sidebarTitles"
      v-on:add-product="addProductItem"
    />
    <Products
      v-if="productsList.length"
      v-bind:productsList="productsList"
      v-on:remove-product="removeProductItem"
    />
    <div class="main__no-products" v-else></div>
  </main>
</template>

<script>
import Sidebar from "@/components/Sidebar";
import Products from "@/components/Products";
import Main from "@/components/Main.vue";

export default {
  props: ["sidebarTitles", "productsList"],
  components: {
    Sidebar,
    Products,
    Main,
  },
  methods: {
    addProductItem(newProduct) {
      this.$emit("add-product", newProduct);
    },
    removeProductItem(productId) {
      this.$emit("remove-product", productId);
    },
  },
};
</script>

<style lang="scss" scoped>
.main {
  display: flex;
  width: 100%;
  height: auto;
}

.main_margin {
  margin-top: 16px;
}

.main__no-products {
  display: block;
  width: 100%;
  height: auto;
  background-image: url('../img/shopping-basket.svg');
  background-position: center;
  background-repeat: no-repeat;
  background-size: auto 40%;
}
</style>