<template>
  <div class="sidebar__input__title sidebar__input__title_margin-bottom">
    <span>{{ titleInfo.title }}</span>
    <span v-bind:class="{ display_none: !titleInfo.necessarily }">*</span>
  </div>
</template>

<script>
export default {
  props: ["titleInfo"],
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

.display_none {
  display: none;
}
</style>