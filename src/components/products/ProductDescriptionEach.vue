<template>
  <div
    class="Each-background"
    :class="{ show: active }"
    @click="$emit('close-product-each')"
  />

  <div class="each" :class="{ show: active }">
      <div class="each-close" @click="$emit('close-product-each')">
        X
      </div>

      <div v-if="product" class="product-details">
        <h3 class="text-center">{{ product.name }}</h3>
        <p class="description">{{ product.description }}</p>
        <h3 class="text-center">${{ product.price.toFixed(2) }}</h3>
        <div class="cart-total" v-if="product_total">
          <h3>In Cart</h3>
          <h4>{{ product_total }}</h4>
        </div>
      </div>
    <div class="button-containar">
      <button class="remove" @click="removeFromCart()">remove</button>
      <button class="add" @click="addToCart()">Add</button>
    </div>
  </div>
</template>
<script>
export default {
  props: ["product", "active"],
  methods: {
    addToCart() {
      this.$store.commit("addToCart", this.product);
    },
    removeFromCart() {
      this.$store.commit("removeFromCart", this.product);
    },
  },
  computed: {
    product_total() {
      return this.$store.getters.productQuantity(this.product);
    },
  },
};
</script>
<style lang="scss">
.Each-background {
  width: 100%;
  height: 100vh;
  position: fixed;
  left: 0;
  top: 0;
  background-color: rgba(124, 124, 125, 0.6);
  z-index: 100;
  display: none;
  transition: display .5s;
  &.show {
    display: block;
  }
 
 
}
.each {
    width: 90vw;
    height: 100vh;
    background-color: white;
    position: fixed;
    top: 0;
    left: -105vw;
    padding: 15px;
    transition: left .6s;
    z-index: 101;
    overflow-y: scroll;
    &.show {
      left: 0;
    }
  }
 .each-close {
    font-size: 1.5rem;
    padding: 5px;
    border: 2px solid gray;
    right: 10px;
    border-radius: 5px;
    color: gray;
    width: 15px;
    float: right;
    cursor: pointer;
    &:hover {
      background-color: blue;
    }
  }
 
.product-details {
  display: flex;
  justify-content: center;
  flex-direction: column;

  p.description {
    padding: 20px;
    line-height: 1.5rem;
  }
  .button-containar {
    button {
      width: 150px;
      border: none;
      padding: 10px;
      border-radius: 5px;
      margin: 0 5px 50px 5px;
      cursor: pointer;
    }
  }
}

@media (min-width: 500px) {
  .each {
    width: 450px;
  }
}
</style>