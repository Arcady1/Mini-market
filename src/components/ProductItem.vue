<template>
  <div class="product__wrapper product__wrapper_margin">
    <div class="product__image__wrapper">
      <img
        class="product__image"
        v-bind:src="product.imageLink"
        @error="
          $event.target.src =
            'https://image.flaticon.com/icons/png/512/2088/2088090.png'
        "
      />
    </div>
    <div
      class="product__non-image__wrapper product__non-image__wrapper_padding"
    >
      <div class="product__remove" v-on:click="removeProd"></div>
      <div class="product__title">{{ product.name }}</div>
      <div class="product__subtitle product__subtitle_margin">
        {{ product.descr }}
      </div>
      <div class="product__price">
        <span>{{ product.priceStr }}</span> <span>руб.</span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["product"],
  methods: {
    removeProd() {
      this.$emit("remove-product-item", this.product.id);
    },
  },
};
</script>

<style lang="scss" scoped>
@import "../style/templ";
@import "../style/mixin";

.product__wrapper {
  display: block;
  width: 100%;
  min-width: 250px;
  max-width: 332px;
  height: 423px;
  background-color: #fffefb;
  box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04),
    0px 6px 10px rgba(0, 0, 0, 0.02);
  border-radius: 4px;
  transition: var(--main-transition);
  position: relative;
  top: 0;
  left: 0;

  .product__remove {
    display: block;
    width: 2rem;
    height: 2rem;
    position: absolute;
    top: -0.5rem;
    right: -0.5rem;
    box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.1);
    border-radius: 10px;
    transition: var(--main-transition);

    @include backgroud-img(url("../img/delete-img.svg"), auto 1rem, #ff8484);
  }

  .product__remove:hover {
    cursor: pointer;
    background-color: #ff6b6b;
  }

  .product__image__wrapper {
    display: block;
    width: 100%;
    height: 47.285%;
    border-radius: 4px;
    overflow: hidden;
    background-color: var(--product-image-bgc);

    .product__image {
      display: block;
      width: auto;
      height: 100%;
      margin: 0 auto;
    }
  }

  .product__non-image__wrapper {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    width: 100%;
    height: calc(100% - 47.285%);

    .product__title {
      @extend %product-title-font;
    }

    .product__subtitle {
      @extend %product-description-font;
    }

    .product__subtitle_margin {
      margin-top: calc(min(5.5%, 16px));
      margin-bottom: calc(min(10.7%, 32px));
    }

    .product__price {
      @extend %product-price-font;
    }
  }

  .product__non-image__wrapper_padding {
    padding: calc(min(5%, 16px));
    padding-bottom: calc(min(7.5%, 24px));
  }
}

.product__wrapper:hover {
  cursor: pointer;
  background-color: var(--product-image-bgc);
  top: 5px;
  left: 0;
}

.product__wrapper_margin {
  margin-bottom: 16px;
}
</style>