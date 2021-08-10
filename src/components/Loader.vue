<template>
  <div class="loader__wrapper">
    <div class="lds-dual-ring"></div>
  </div>
</template>

<style lang="scss" scoped>
$loader-color: #000;

.loader__wrapper {
  display: -webkit-box;
  display: flex;
  -webkit-box-pack: center;
  justify-content: center;
  -webkit-box-align: center;
  align-items: center;
  width: 100%;
  height: auto;
}

.lds-dual-ring {
  display: inline-block;
  width: 80px;
  height: 80px;
}

.lds-dual-ring:after {
  content: " ";
  display: block;
  width: 64px;
  height: 64px;
  margin: 8px;
  border-radius: 50%;
  border: 6px solid $loader-color;
  border-color: $loader-color transparent $loader-color transparent;
  -webkit-animation: lds-dual-ring 1.2s linear infinite;
  animation: lds-dual-ring 1.2s linear infinite;
}

@-webkit-keyframes lds-dual-ring {
  0% {
    -webkit-transform: rotate(0deg);
    transform: rotate(0deg);
  }

  100% {
    -webkit-transform: rotate(360deg);
    transform: rotate(360deg);
  }
}

@keyframes lds-dual-ring {
  0% {
    -webkit-transform: rotate(0deg);
    transform: rotate(0deg);
  }

  100% {
    -webkit-transform: rotate(360deg);
    transform: rotate(360deg);
  }
}
</style>