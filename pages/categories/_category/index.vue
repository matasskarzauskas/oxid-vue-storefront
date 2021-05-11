<template>
  <div class="container">
    <div
      v-for="product in categories[0].products"
      class="grid grid-cols-1 md:grid-cols-6"
      v-bind:key="product.id"
    >
      {{ product.title }}
    </div>
    {{ categories.products }}
  </div>
</template>

<script>
const CATEGORY_PRODUCTS = require('../../../apollo/queries/categories/category_products.gql')

export default {
  name: 'Category',
  apollo: {
    categories: {
      query: CATEGORY_PRODUCTS,
      variables() {
        return {
          category: this.$route.params.category,
        }
      },
      result(data) {
        console.log(data)
      },
    },
  },
  data() {
    return {
      categoryTree: [],
    }
  },
  methods: {},
}
</script>

<style>
/* Sample `apply` at-rules with Tailwind CSS
.container {
@apply min-h-screen flex justify-center items-center text-center mx-auto;
}
*/
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
