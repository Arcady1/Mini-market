<template>
  <div class="product__wrapper product__wrapper_margin">
    <div class="product__image"></div>
    <div
      class="product__non-image__wrapper product__non-image__wrapper_padding"
    >
      <div class="product__remove"></div>
      <div class="product__title">Наименование товара</div>
      <div class="product__subtitle product__subtitle_margin">
        Довольно-таки интересное описание товара в несколько строк.
        Довольно-таки интересное описание товара в несколько строк
      </div>
      <div class="product__price">10 000 руб.</div>
    </div>
  </div>
</template>

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

  .product__image {
    display: block;
    width: 100%;
    height: 47.285%;
    border-radius: 4px;

    @include backgroud-img(
      url("https://icdn.digitaltrends.com/image/digitaltrends/gopro-hero9-black-review-dm-6-2.jpg"),
      auto 100%,
      var(--product-image-bgc)
    );
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