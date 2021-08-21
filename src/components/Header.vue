<template>
  <header class="header">
    <h1 class="header__title">Adding a product</h1>
    <div class="header__filter">
      <button
        class="filter__title filter__title_margin filter__element_padding"
      >
        <span>{{ filterIdToText }}</span>
        <span class="filter__arrow"></span>
      </button>
      <div class="filter__menu">
        <HeaderFilterItem
          v-for="filter in filters"
          v-bind:key="filter.id"
          v-bind:filter="filter"
          v-on:products-sort="productsSort"
        />
      </div>
    </div>
  </header>
</template>

<script>
import HeaderFilterItem from "@/components/HeaderFilterItem";

export default {
  props: ["sortFilterId"],
  data() {
    return {
      filters: [
        {
          name: "By default",
          id: 0,
        },
        {
          name: "Price min",
          id: 1,
        },
        {
          name: "Price max",
          id: 2,
        },
        {
          name: "By name",
          id: 3,
        },
      ],
    };
  },
  components: {
    HeaderFilterItem,
  },
  computed: {
    filterIdToText() {
      const filterObj = this.filters.find(
        (filterObj) => filterObj.id === this.sortFilterId
      );

      return filterObj.name;
    },
  },
  methods: {
    productsSort(filterId) {
      this.$emit("product-sort", filterId);
    },
  },
};
</script>

<style lang="scss" scoped>
@import "../style/templ";

.header {
  display: -webkit-box;
  display: flex;
  -webkit-box-pack: justify;
  justify-content: space-between;
  width: 100%;
  height: auto;

  .header__title {
    @extend %title-font;

    display: -webkit-box;

    display: flex;
    -webkit-box-orient: vertical;
    -webkit-box-direction: normal;
    flex-direction: column;
    -webkit-box-pack: center;
    justify-content: center;
  }

  .header__filter {
    @extend %filter-font;
    @extend %filter-style;

    display: block;
    width: 121.49px;
    height: 36px;
    position: relative;

    .filter__title {
      display: -webkit-box;
      display: flex;
      -webkit-box-pack: justify;
      justify-content: space-between;
      -webkit-box-align: center;
      align-items: center;
      width: 100%;
      height: 100%;
      -webkit-transition: var(--main-transition);
      transition: var(--main-transition);
      color: inherit;
      font-size: inherit;

      .filter__arrow {
        display: block;
        width: 4.59px;
        height: 4.59px;
        border: solid #b4b4b4;
        border-width: 0 1px 1px 0;
        -webkit-transform: rotate(45deg);
        transform: rotate(45deg);
        -webkit-transition: var(--main-transition);
        transition: var(--main-transition);
      }
    }

    .filter__title:hover {
      color: #000;

      .filter__arrow {
        border-color: #000;
      }
    }

    .filter__element_padding {
      padding: 11px 12px 10px 12px;
    }

    .filter__menu {
      @extend %filter-style;

      width: 100%;
      opacity: 0;
      position: absolute;
      -webkit-transform: scaleY(0);
      transform: scaleY(0);
      -webkit-transform-origin: 0 0;
      transform-origin: 0 0;
      -webkit-transition: var(--main-transition);
      transition: var(--main-transition);
      z-index: 1;
      text-align: center;
    }
  }

  .header__filter:hover .filter__menu {
    -webkit-transform: scaleY(1);
    transform: scaleY(1);
    opacity: 1;
  }
}
</style>
