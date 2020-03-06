<template>
  <div>
    <h2>{{ ifEmpty }}</h2>
    <CartItem
      v-for="product in cart"
      :product="product"
      :key="product.id"
      @updateItemQuantity="updateItemQuantity"
      @removeItem="removeItem"
    />
  </div>
</template>

<script>
import CartItem from "../components/CartItem.vue";

export default {
  name: "CartPage",
  components: {
    CartItem
  },
  props: {
    cart: {
      type: Array
    }
  },
  methods: {
    updateItemQuantity(id, quantity) {
      this.$emit("updateItemQuantity", id, quantity);
    },
    removeItem(id) {
      this.$emit("removeItem", id);
    }
  },
  computed: {
    ifEmpty() {
      return this.cart.length === 0 ? "Cart is empty" : undefined;
    }
  }
};
</script>

<style scoped>
</style>

