<template>
  <div id="app">
    <div class="wrapper">
      <app-burger />
    </div>
    <div class="controls">
      <h2 class="mb-5">Ingredients</h2>
      <app-beef-patty-controls />
      <app-chicken-patty-controls />
      <app-cheese-controls />
      <app-bacon-controls />
      <app-lettuce-controls />
    </div>
  </div>
</template>

<script>
import Burger from "./views/Burger.vue";
import BeefPattyControls from "./components/BeefPattyControls.vue";
import ChickenPattyControls from "./components/ChickenPattyControls.vue";
import CheeseControls from "./components/CheeseControls.vue";
import BaconControls from "./components/BaconControls.vue";
import LettuceControls from "./components/LettuceControls.vue";

export default {
  name: "app",
  components: {
    AppBurger: Burger,
    AppBeefPattyControls: BeefPattyControls,
    AppChickenPattyControls: ChickenPattyControls,
    AppCheeseControls: CheeseControls,
    AppBaconControls: BaconControls,
    AppLettuceControls: LettuceControls
  }
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
}

#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
.wrapper {
  display: flex;
  box-sizing: border-box;
  min-height: 100vh;
  width: 80vw;
  align-items: center;
  justify-content: center;
  background-color: #000;
  padding: 50px 0;
}

.controls {
  box-sizing: border-box;
  padding: 2%;
  width: 20vw;
  height: 100vh;
  position: absolute;
  top: 0;
  right: 0;
  background-color: #333;
  display: flex;
  flex-direction: column;
  color: #fff;
  justify-content: center;
}

.controls h4 {
  line-height: 38px;
}
</style>
