<template>
  <div>
    <Header v-on:product-sort="productsSort" />
    <Main />
  </div>
</template>

<script>
import Header from "@/components/Header";
import Main from "@/components/Main";

export default {
  name: "App",
  data() {
    return {
      sortFilterId: null,
    };
  },
  components: {
    Header,
    Main,
  },
  methods: {
    productsSort(sortId) {
      sortFilterId = sortId;
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
