<template>
  <div>
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
    commerce: {
      type: Object,
      required: true
    },
    cart: {
      type: Array
    }
  },
  methods: {
    updateItemQuantity(id, quantity) {
        this.$emit("updateItemQuantity", id, quantity)
    },
    removeItem(id) {
        this.$emit("removeItem", id)
    }
  }
};
</script>

<style scoped>
</style>

