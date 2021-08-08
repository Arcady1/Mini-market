<template>
  <form class="sidebar sidebar_padding sidebar_margin-right">
    <!-- Наименование товара -->
    <div class="sidebar__input__wrapper sidebar__input__wrapper_margin">
      <SidebarInputTitle v-bind:title="sidebarTitles[0].title" />
      <input
        type="text"
        class="sidebar__input sidebar__input_padding"
        id="inputProductName"
        placeholder="Введите наименование товара"
        required
        pattern="(\s*[a-zA-Zа-яА-Я0-9]+\s*)+"
        v-on:input="inputChangeHandler($event)"
      />
      <p class="sidebar__input__invalid">Поле является обязательным</p>
    </div>
    <!-- Описание товара -->
    <div class="sidebar__input__wrapper sidebar__input__wrapper_margin">
      <SidebarInputTitle v-bind:title="sidebarTitles[1].title" />
      <textarea
        cols="10"
        rows="6"
        placeholder="Введите описание товара"
        class="sidebar__input sidebar__input__textarea sidebar__input_padding"
      ></textarea>
      <p class="sidebar__input__invalid">Поле является обязательным</p>
    </div>
    <!-- Ссылка на изображение товара -->
    <div class="sidebar__input__wrapper sidebar__input__wrapper_margin">
      <SidebarInputTitle v-bind:title="sidebarTitles[2].title" />
      <input
        type="text"
        class="sidebar__input sidebar__input_padding"
        id="inputProductLink"
        placeholder="Введите ссылку"
        required
        pattern="^\S*$"
        v-on:input="inputChangeHandler($event)"
      />
      <p class="sidebar__input__invalid">Поле является обязательным</p>
    </div>
    <!-- Цена товара -->
    <div class="sidebar__input__wrapper sidebar__input__wrapper_margin">
      <SidebarInputTitle v-bind:title="sidebarTitles[3].title" />
      <input
        type="text"
        class="sidebar__input sidebar__input_padding"
        id="inputProductPrice"
        placeholder="Введите цену"
        required
        pattern="(\d+ *)+"
        v-on:input="inputChangeHandler($event)"
        v-model="input.inputPrice"
      />
      <p class="sidebar__input__invalid">Поле является обязательным</p>
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
      @click.prevent
    >
      Добавить товар
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
        inputPrice: null,
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

      if (elem.validity.valid) {
        correctObj[elem.id] = true;
      } else {
        correctObj[elem.id] = false;
      }

      if (
        correctObj.inputProductName &&
        correctObj.inputProductLink &&
        correctObj.inputProductPrice
      ) {
        this.isButtonActive = true;
      } else {
        this.isButtonActive = false;
      }

      const price = this.input.inputPrice.replace(/ /g, "");

      if (price && !isNaN(price - 0)) {
        this.input.inputPrice = (price - 0).toLocaleString().replace(/,/g, " ");
      }
    },
  },
};
</script>

<style lang="scss" scoped>
@import "../style/templ";

.sidebar {
  display: flex;
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
      transition: var(--main-transition);
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
      transition: var(--main-transition);
    }

    .sidebar__input:not(:placeholder-shown) {
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
  div span:nth-child(2) {
    display: none;
  }

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