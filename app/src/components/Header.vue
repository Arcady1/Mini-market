<template>
  <header class="header">
    <h1 class="header__title">Добавление товара</h1>
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
  // filters: {
  //   filterIdToText(filterId) {
  //     console.log(filterId);
  //     return filterId + 20;
  //   },
  // },
  data() {
    return {
      filters: [
        {
          name: "По умолчанию",
          id: 0,
        },
        {
          name: "По возрастанию цены",
          id: 1,
        },
        {
          name: "По убыванию цены",
          id: 2,
        },
        {
          name: "По наименованию",
          id: 3,
        },
      ],
      currentFilter: "По умолчанию",
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
  display: flex;
  justify-content: space-between;
  width: 100%;
  height: auto;

  .header__title {
    @extend %title-font;

    display: flex;
    flex-direction: column;
    justify-content: center;
  }

  .header__filter {
    @extend %filter-font;
    @extend %filter-style;

    display: block;
    width: auto;
    height: 36px;
    position: relative;

    .filter__title {
      display: flex;
      justify-content: space-between;
      align-items: center;
      width: 100%;
      height: 100%;
      transition: var(--main-transition);
      color: inherit;

      .filter__arrow {
        display: block;
        width: 4.59px;
        height: 4.59px;
        border: solid #b4b4b4;
        border-width: 0 1px 1px 0;
        transform: rotate(45deg);
        transition: var(--main-transition);
      }
    }

    .filter__title_margin {
      margin-right: 5px;
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
      top: -610%;
      transition: var(--main-transition);
      z-index: 1;
      text-align: center;
    }
  }

  .header__filter:hover .filter__menu {
    top: 100%;
    opacity: 1;
  }
}
</style>