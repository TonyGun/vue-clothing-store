<template>
  <div class="catalog">
    <h2>Product catalog</h2>
    <catalog-filter />
    <div class="catalog__body">
      <div class="catalog__bacground-v"></div>
      <side-bar />
      <div v-if="products.length" class="catalog__items container">
        <product-card
          v-for="product in products"
          :key="product.id"
          :product="product" 
          @click.native="goToProduct(product.id)" 
        />
      </div>
    </div>
  </div>
</template>

<script>
import ProductCard from '@/components/widgets/product/ProductCard'
import SideBar from '@/components/SideBar'
import CatalogFilter from '@/components/CatalogFilter'

export default {
  name: 'CatalogPage',
  
  components: { 
    ProductCard, 
    SideBar,
    CatalogFilter
  },

  computed: {
    products() {
      return this.$store.getters['productList']
    },
  },

  methods: {
    goToProduct(id) {
      this.$router.push({
        name: 'product', 
        params: { id }
      })
    },

    getProducts() {
      this.$store.dispatch('getProducts')
    }
  },

  created() {
    this.getProducts()
  }
}
</script>

<style lang="scss" scoped>
.catalog {
  &__body {
    position: relative;
  }
  &__bacground-v {
    opacity: 0.2;
    z-index: -1;
    height: 100%;
    width: 100%;
    position: absolute;
    background: url('https://upload.wikimedia.org/wikipedia/commons/9/95/Vue.js_Logo_2.svg') no-repeat top center;
  }
  &__items {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-around;
  }
}
</style>