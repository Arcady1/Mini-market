<template>
  <header class="header">
    <h1 class="header__title">Добавление товара</h1>
    <div class="header__filter">
      <button class="filter__title filter__element_padding">
        <span>По умолчанию</span>
        <span class="filter__arrow"></span>
      </button>
      <div class="filter__menu">
        <li class="filter__element_padding">По возрастанию цены</li>
        <li class="filter__element_padding">По убыванию цены</li>
        <li class="filter__element_padding">По наименованию</li>
      </div>
    </div>
  </header>
</template>

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
    width: 121.49px;
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

      opacity: 0;
      position: absolute;
      top: -100vh;
      transition: var(--main-transition);
      z-index: 1;
      text-align: center;
    }

    .filter__menu li {
      display: block;
      transition: var(--main-transition);
      color: inherit;
    }

    .filter__menu li:hover {
      cursor: pointer;
      color: #000;
    }
  }

  .header__filter:hover .filter__menu {
    top: 100%;
    opacity: 1;
  }
}
</style>