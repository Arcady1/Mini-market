<template>
  <div>
    <Header
      v-on:product-sort="productsSort"
      v-bind:sortFilterId="sortFilterId"
    />
    <Main
      v-on:add-product="addProduct"
      v-on:remove-product="removeProduct"
      v-bind:sidebarTitles="sidebarTitles"
      v-bind:productsList="productsList"
    />
  </div>
</template>

<script>
import Header from "@/components/Header";
import Main from "@/components/Main";

export default {
  name: "App",
  data() {
    return {
      sidebarTitles: [
        { title: "Наименование товара", necessarily: true },
        { title: "Описание товара", necessarily: false },
        { title: "Ссылка на изображение товара", necessarily: true },
        { title: "Цена товара", necessarily: true },
      ],
      productsList: [],
      sortFilterId: 0,
    };
  },
  // mounted() {},
  components: {
    Header,
    Main,
  },
  mounted() {
    this.productsList = JSON.parse(localStorage.getItem("productsList"));
  },
  methods: {
    // Product sorting method
    productsSort(sortId) {
      this.sortFilterId = sortId;

      console.log(this.sortFilterId);

      // Sorting by increasing price
      if (this.sortFilterId === 1) {
        this.productsList.sort((a, b) => a.price - b.price);
      }
      // Sorting by decreasing price
      else if (this.sortFilterId === 2) {
        this.productsList.sort((a, b) => b.price - a.price);
      }
      // Sorting by increasing name
      else if (this.sortFilterId === 0 || this.sortFilterId === 3) {
        this.productsList.sort((a, b) => {
          let nameA = a.name.toLowerCase();
          let nameB = b.name.toLowerCase();

          if (nameA < nameB) return -1;
          else if (nameA > nameB) return 1;
          else return 0;
        });
      }
    },
    // Add product method
    addProduct(newProduct) {
      this.productsList.push(newProduct);
      this.productsListToLocalStorage();
    },
    // Remove product method
    removeProduct(productId) {
      this.productsList = this.productsList.filter(
        (product) => product.id !== productId
      );
      this.productsListToLocalStorage();
    },
    // Set productsList to localStorage
    productsListToLocalStorage() {
      localStorage.setItem("productsList", JSON.stringify(this.productsList));
    },
  },
};
</script>

<style lang="scss">
@import "./style/common";
@import "./style/mixin";

body {
  background-color: var(--main-bgc);
}

.content__wrapper {
  display: block;
  width: 100%;
  min-width: var(--min-width);
  max-width: var(--max-width);
  height: auto;
  background-color: var(--main-bgc);

  .content {
    display: block;
    width: 100%;
    height: auto;
    background-color: var(--main-bgc);
  }
}

.content_padding {
  padding: calc(10px + 22 * (100% - 320px) / (1440 - 320));
  padding-bottom: 0;
}

.content__wrapper_margin {
  margin: 0 auto;
}
</style>
