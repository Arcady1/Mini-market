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
      productsList: {
        // id: {
        //   id: new Date() - 0 + Math.random(),
        //   name: this.input.info.name,
        //   descr: this.input.info.descr,
        //   imageLink: this.input.info.link,
        //   price: this.input.info.price,
        // },
      },
    };
  },
  components: {
    Sidebar,
    Products,
    Main,
  },
  methods: {
    addProductItem(newProduct) {
      this.productsList[newProduct.id] = newProduct;
    },
    removeProductItem(productId) {
      delete this.productsList[productId];
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