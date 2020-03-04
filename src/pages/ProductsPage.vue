<template>
  <div>
    <Product
      v-for="product in products"
      :product="product"
      :key="product.id"
      @viewProduct="handleViewProduct"
    />
  </div>
</template>

<script>
import Product from "../components/Product.vue";

export default {
  name: "ProductsPage",
  components: {
    Product
  },
  props: {
    products: {
      type: Array
    }
  },
  methods: {
    handleViewProduct(product) {
      this.$emit("handleViewProduct", product);
    }
  }
  // created() {
  //   this.commerce.products
  //     .list()
  //     .then(res => {
  //       console.log(res.data);
  //       this.products = res.data;
  //     })
  //     .catch(err => console.log(err));
  // }
};
</script>

<style scoped>
</style>

