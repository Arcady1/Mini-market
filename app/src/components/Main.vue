<template>
  <main class="main main_margin">
    <Sidebar
      v-bind:sidebarTitles="sidebarTitles"
      v-on:add-product="addProductItem"
    />
    <Products
      v-bind:productsList="productsList"
      v-on:remove-product="removeProductItem"
    />
  </main>
</template>

<script>
import Sidebar from "@/components/Sidebar";
import Products from "@/components/Products";
import Main from "@/components/Main.vue";

export default {
  data() {
    return {
      sidebarTitles: [
        { title: "Наименование товара", necessarily: true },
        { title: "Описание товара", necessarily: false },
        { title: "Ссылка на изображение товара", necessarily: true },
        { title: "Цена товара", necessarily: true },
      ],
      productsList: [],
    };
  },
  components: {
    Sidebar,
    Products,
    Main,
  },
  methods: {
    addProductItem(newProduct) {
      this.productsList.push(newProduct);
    },
    removeProductItem(productId) {
      this.productsList = this.productsList.filter(
        (product) => product.id !== productId
      );
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
</style>