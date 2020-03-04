<template>
  <div class="container">
    <!-- <p v-for="product in products" :key="product.id"/> -->
    <Header />
    <router-view
      :productInView="productInView"
      :products="products"
      @handleViewProduct="setProductInView"
      :cart="cart"
      @updateItemQuantity="handleUpdateItemQuantity"
      @removeItem="handleRemoveItem"
      @addProductToCart="handleAddProductToCart"
      :status="status"
    />
  </div>
</template>

<script>
import Header from "./components/Header";
export default {
  name: "App",
  // declare props property in child compoent so
  // it knows it's receiving props
  props: {
    commerce: {
      type: Object,
      required: true
    }
  },
  components: {
    Header
  },
  // data is to store state data
  data() {
    return {
      products: [],
      productInView: {},
      cart: [],
      status: undefined
    };
  },
  methods: {
    setProductInView(product) {
      this.productInView = product;
      this.status = undefined
    },
    handleUpdateItemQuantity(id, quantity) {
      this.commerce.cart.update(id, { quantity })
        .then((res) => {
          this.cart = res.cart.line_items
        })
        .catch(err => console.log(err))
    },
    handleRemoveItem(id) {
      this.commerce.cart.remove(id)
        .then((res) => {
          this.cart = res.cart.line_items
        })
        .catch(err => console.log(err))
    },
    handleAddProductToCart(productInView) {
      this.commerce.cart.add(
        productInView.id
      )
      .then((res) => {
        this.status = "Item added to cart!"
        this.cart = res.cart.line_items
        console.log(res)
      })
      .catch((err) => console.log(err))
    }
  }, // created is called with Vue app is created
  // This is useful for prepopulating data with API calls
  created() {
    this.commerce.products
      .list()
      .then(res => {
        this.products = res.data;
        this.commerce.cart
          .retrieve()
          .then(res => {
            this.cart = res.line_items
          })
          .catch(err => console.log(err))
      })
      .catch(err => console.log(err));
  }
};
</script>

<style>
</style>
