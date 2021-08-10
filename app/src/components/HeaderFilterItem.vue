<template>
  <div>
    <li
      class="filter__element filter__element_padding"
      v-on:click="$emit('products-sort', filter.id)"
    >
      {{ filter.name }}
    </li>
  </div>
</template>

<script>
export default {
  props: ["filter"],
};
</script>

<style lang="scss" scoped>
@import "../style/templ";

.filter__element {
  display: block;
  transition: var(--main-transition);
  color: inherit;
}

.filter__element:hover {
  cursor: pointer;
  color: #000;
}

.filter__element_padding {
  padding: 11px 12px 10px 12px;
}
</style>