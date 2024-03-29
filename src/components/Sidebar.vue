<template>
  <form class="sidebar sidebar_padding sidebar_margin-right">
    <!-- Наименование товара -->
    <div class="sidebar__input__wrapper sidebar__input__wrapper_margin">
      <SidebarInputTitle v-bind:titleInfo="sidebarTitles[0]" />
      <input
        type="text"
        autocomplete="off"
        class="sidebar__input sidebar__input_padding"
        id="inputProductName"
        placeholder="Enter the product name"
        required
        pattern="(\s*\S+\s*)+"
        v-on:input="inputChangeHandler($event)"
        v-model="input.info.name"
      />
      <p class="sidebar__input__invalid">The field is required</p>
    </div>
    <!-- Описание товара -->
    <div class="sidebar__input__wrapper sidebar__input__wrapper_margin">
      <SidebarInputTitle v-bind:titleInfo="sidebarTitles[1]" />
      <textarea
        autocomplete="off"
        cols="10"
        rows="6"
        placeholder="Enter product description"
        class="sidebar__input sidebar__input__textarea sidebar__input_padding"
        v-model="input.info.descr"
      ></textarea>
      <p class="sidebar__input__invalid">The field is required</p>
    </div>
    <!-- Ссылка на изображение товара -->
    <div class="sidebar__input__wrapper sidebar__input__wrapper_margin">
      <SidebarInputTitle v-bind:titleInfo="sidebarTitles[2]" />
      <input
        type="text"
        autocomplete="off"
        class="sidebar__input sidebar__input_padding"
        id="inputProductLink"
        placeholder="Enter the image link"
        required
        pattern="^\S*$"
        v-on:input="inputChangeHandler($event)"
        v-model="input.info.link"
      />
      <p class="sidebar__input__invalid">The field is required</p>
    </div>
    <!-- Цена товара -->
    <div class="sidebar__input__wrapper sidebar__input__wrapper_margin">
      <SidebarInputTitle v-bind:titleInfo="sidebarTitles[3]" />
      <input
        type="text"
        autocomplete="off"
        class="sidebar__input sidebar__input_padding"
        id="inputProductPrice"
        placeholder="Enter the price"
        required
        pattern="(\d+ *)+"
        v-model="input.info.priceStr"
        v-on:input="inputChangeHandler($event)"
      />
      <p class="sidebar__input__invalid">The field is required</p>
    </div>
    <!-- Добавить товар -->
    <button
      class="
        sidebar__button
        sidebar__button_inactive
        sidebar__button_padding
        sidebar__button_margin
      "
      v-bind:class="{ sidebar__button_active: sendButtonActive() }"
      @click.prevent="onSubmit()"
    >
      Add product
    </button>
  </form>
</template>

<script>
import SidebarInputTitle from "@/components/SidebarInputTitle";

export default {
  props: ["sidebarTitles"],
  data() {
    return {
      isButtonActive: false,
      input: {
        correct: {
          inputProductName: false,
          inputProductLink: false,
          inputProductPrice: false,
        },
        info: {
          name: "",
          descr: "",
          link: "",
          priceStr: "",
          price: "",
        },
      },
    };
  },
  components: {
    SidebarInputTitle,
  },
  methods: {
    sendButtonActive() {
      return this.isButtonActive;
    },
    inputChangeHandler(event) {
      const elem = event.target;
      const correctObj = this.input.correct;

      this.setInputStatus(elem, correctObj);
      this.submitButtonActivate(correctObj);
      this.priceThousandsSeparation(elem);
    },
    // Set input status: correct / incorrect
    setInputStatus(elem, correctObj) {
      if (elem.validity.valid) {
        correctObj[elem.id] = true;
      } else {
        correctObj[elem.id] = false;
      }
    },
    // Activate the submit button if all input fields are correct
    submitButtonActivate(correctObj) {
      if (
        correctObj.inputProductName &&
        correctObj.inputProductLink &&
        correctObj.inputProductPrice
      ) {
        this.isButtonActive = true;
      } else {
        this.isButtonActive = false;
      }
    },
    // Thousands space separation mask for the price field
    priceThousandsSeparation(elem) {
      if (elem.id === "inputProductPrice") {
        let priceStr = this.input.info.priceStr.replace(/ /g, "");

        if (priceStr && !isNaN(priceStr - 0)) {
          this.input.info.price = priceStr - 0;
          this.input.info.priceStr = this.input.info.price
            .toLocaleString()
            .replace(/,/g, " ");
        }
      }
    },
    onSubmit() {
      // Check Send button for activity
      if (!this.isButtonActive) {
        return false;
      }

      const input = this.input;
      // Generating a new product
      const newProductItem = {
        id: new Date() - 0 + Math.random(),
        name: input.info.name,
        descr: input.info.descr,
        imageLink: input.info.link,
        priceStr: input.info.priceStr,
        price: input.info.price,
      };

      this.inputClean(input);
      this.inputStatusReset(input);

      // Deactivating the send button
      this.isButtonActive = false;
      // Adding a new product
      this.$emit("add-product", newProductItem);
    },
    // Input fields cleaning
    inputClean(input) {
      for (let key in input.info) {
        input.info[key] = "";
      }
    },
    // Input status reset
    inputStatusReset(input) {
      // Input status incorrect
      for (let key in input.correct) {
        input.correct[key] = false;
      }
    },
  },
};
</script>

<style lang="scss" scoped>
@import "../style/templ";

.sidebar {
  display: -webkit-box;
  display: flex;
  -webkit-box-orient: vertical;
  -webkit-box-direction: normal;
  flex-direction: column;
  width: 100%;
  min-width: 161px;
  max-width: 332px;
  height: 1%;
  background-color: #fffefb;
  box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04),
    0px 6px 10px rgba(0, 0, 0, 0.02);
  border-radius: 4px;

  .sidebar__input__wrapper {
    display: block;
    width: 100%;
    height: auto;
    position: relative;

    .sidebar__input__textarea {
      height: 108px;
      resize: none;
    }

    .sidebar__input {
      @extend %filter-input-font;

      display: block;
      width: 100%;
      background-color: #fffefb;
      box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
      border-radius: 4px;
      border: 1px solid transparent;
      -webkit-transition: var(--main-transition);
      transition: var(--main-transition);
    }

    .sidebar__input::-webkit-input-placeholder {
      color: #b4b4b4;
    }

    .sidebar__input::-moz-placeholder {
      color: #b4b4b4;
    }

    .sidebar__input:-ms-input-placeholder {
      color: #b4b4b4;
    }

    .sidebar__input::-ms-input-placeholder {
      color: #b4b4b4;
    }

    .sidebar__input::placeholder {
      color: #b4b4b4;
    }

    .sidebar__input:focus {
      border-color: var(--button-active-color);
    }

    .sidebar__input__invalid {
      @extend %sidebar-input-invalid-font;

      display: block;
      position: absolute;
      width: 100%;
      height: auto;
      opacity: 0;
      -webkit-transition: var(--main-transition);
      transition: var(--main-transition);
    }

    .sidebar__input:not(:placeholder-shown) {
      -webkit-transition: none;
      transition: none;

      color: #3f3f3f;
    }

    .sidebar__input:invalid:not(:placeholder-shown) {
      border: 1px solid #ff8484;

      & ~ .sidebar__input__invalid {
        opacity: 1;
      }
    }

    .sidebar__input_padding {
      padding: 10px 16px 11px 10px;
    }
  }

  .sidebar__button {
    @extend %filter-button-font;

    display: block;
    width: 100%;
    height: auto;
    border-radius: 10px;
    -webkit-transition: var(--main-transition);
    transition: var(--main-transition);
  }

  .sidebar__button_margin {
    margin-top: calc(min(8.455%, 24px));
    margin-bottom: calc(min(8.455%, 24px));
  }

  .sidebar__button_inactive {
    cursor: default;
    background-color: var(--button-inactive-color);
  }

  .sidebar__button_active {
    background-color: var(--button-active-color);
    color: #fff;
  }

  .sidebar__button_active:hover {
    cursor: pointer;
    background-color: var(--button-active--hover-color);
  }

  .sidebar__button_padding {
    padding: 10px 16px 10px 16px;
  }
}

.sidebar__input__wrapper:nth-child(2) {
  .sidebar__input__invalid {
    display: none;
  }
}

.sidebar__input__wrapper_margin {
  margin-top: 16px;
}

.sidebar__input__wrapper_margin:first-child {
  margin-top: 0;
}

.sidebar_padding {
  padding: calc(min(1.76%, 24px));
  padding-bottom: 0;
}

.sidebar_margin-right {
  margin-right: 16px;
}
</style>