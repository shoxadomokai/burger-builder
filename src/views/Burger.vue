<template>
  <div class="box">
    <app-burger-bottom :key="'burger-top'" />
    <transition-group
      @enter="enter"
      @after-enter="afterEnter"
      @leave="leave"
      class="box"
      name="expand"
      mode="out-in"
    >
      <h2
        :key="'please'"
        v-if="order.length == 0"
        style="height: 200px; color: #fff; line-height: 200px"
      >Please start adding ingredients</h2>
      <component
        v-else
        :key="order[n-1]"
        v-for="n in order.length"
        :is="order[n-1]"
        :order="order"
      />
    </transition-group>
    <app-burger-top :key="'burger-bottom'" />
  </div>
</template>

<script>
import BurgerTop from "../components/BurgerTop.vue";
import BurgerBottom from "../components/BurgerBottom.vue";
import BeefPatty from "../components/BeefPatty.vue";
import Cheese from "../components/Cheese.vue";
import Bacon from "../components/Bacon.vue";
import Lettuce from "../components/Lettuce.vue";
import ChickenPatty from "../components/ChickenPatty.vue";

import { eventBus } from "../main";

export default {
  components: {
    AppBurgerTop: BurgerTop,
    AppBurgerBottom: BurgerBottom,
    AppBeefPatty: BeefPatty,
    AppCheese: Cheese,
    AppBacon: Bacon,
    AppLettuce: Lettuce,
    AppChickenPatty: ChickenPatty
  },
  data() {
    return {
      order: []
    };
  },
  methods: {
    enter(element) {
      const width = getComputedStyle(element).width;

      element.style.width = width;
      element.style.position = "absolute";
      element.style.visibility = "hidden";
      element.style.height = "auto";

      const height = getComputedStyle(element).height;

      element.style.width = null;
      element.style.position = null;
      element.style.visibility = null;
      element.style.height = 0;

      // Force repaint to make sure the
      // animation is triggered correctly.
      getComputedStyle(element).height;

      // Trigger the animation.
      // We use `setTimeout` because we need
      // to make sure the browser has finished
      // painting after setting the `height`
      // to `0` in the line above.
      setTimeout(() => {
        element.style.height = height;
      });
    },
    afterEnter(element) {
      element.style.height = "auto";
    },
    leave(element) {
      const height = getComputedStyle(element).height;

      element.style.height = height;

      // Force repaint to make sure the
      // animation is triggered correctly.
      getComputedStyle(element).height;

      setTimeout(() => {
        element.style.height = 0;
      });
    }
  },
  created() {
    eventBus.$on("newItem", data => {
      this.order.push(data);
    });
    eventBus.$on("removeItem", data => {
      for (var i = this.order.length; i >= 0; i--) {
        if (this.order[i] === data) {
          this.order.splice(i, 1);
          break;
        }
      }
    });
  }
};
</script>

<style lang="css" scoped>
* {
  will-change: height;
  transform: translateZ(0);
  backface-visibility: hidden;
  perspective: 1000px;
}
.box {
  display: flex;
  flex-direction: column-reverse;
}
.expand-enter-active,
.expand-leave-active {
  transition: all 0.4s ease;
  overflow: hidden;
  opacity: 1;
}

.expand-enter,
.expand-leave-to {
  height: 0;
  opacity: 0;
}
</style>