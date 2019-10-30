<template>
  <div class="mb-4">
    <h6>Lettuce</h6>
    <div class="row justify-content-center">
      <div class="col-md-5">
        <button class="btn btn-danger btn-block" @click="removeOrder">Remove</button>
      </div>
      <div class="col-md-2 text-center">
        <h4>{{amount}}</h4>
      </div>
      <div class="col-md-5">
        <button class="btn btn-primary btn-block" @click="addOrder">Add</button>
      </div>
    </div>
  </div>
</template>

<script>
import { eventBus } from "../main";
export default {
  data() {
    return {
      amount: 0
    };
  },
  methods: {
    addOrder() {
      this.amount++;
      eventBus.$emit("newItem", "app-lettuce");
    },
    removeOrder() {
      if (this.amount > 0) {
        this.amount--;
        eventBus.$emit("removeItem", "app-lettuce");
      }
    }
  }
};
</script>

<style scoped>
</style>