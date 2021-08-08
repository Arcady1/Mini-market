<template>
  <main class="main main_margin">
    <Sidebar v-bind:sidebarTitles="sidebarTitles" />
    <Products />
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
        { title: "Наименование товара" },
        { title: "Описание товара" },
        { title: "Ссылка на изображение товара" },
        { title: "Цена товара" },
      ],
    };
  },
  components: {
    Sidebar,
    Products,
    Main,
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