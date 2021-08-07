<template>
  <div class="sidebar__input__title sidebar__input__title_margin-bottom">
    <span>{{ title }}</span>
    <span>*</span>
  </div>
</template>

<script>
export default {
  props: ["title"],
};
</script>

<style lang="scss" scoped>
@import "../style/templ";

.sidebar__input__title {
  @extend %filter-title-font;

  display: block;
  width: auto;
}

.sidebar__input__title span:nth-child(2) {
  color: #ff8484;
  border-radius: 4px;
}

.sidebar__input__title_margin-bottom {
  margin-bottom: 4px;
}
</style>