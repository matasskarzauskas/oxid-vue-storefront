<template>
  <div>
    <div class="h-10 w-full bg-gray-100 flex items-center justify-start pl-5">
      <div
        class="max-w-7xl mx-auto px-2 sm:px-6 lg:px-8 font-medium text-gray-400"
      >
        <span>{{ $route.params.category }}</span>
        <span class="font-medium">/</span>
        <span>{{ $route.params.subcategory }}</span>
      </div>
    </div>
    <div class="container flex items-center justify-center">
      <div
        class="grid grid-cols-1 md:grid-cols-4 gap-5 mt-4"
        v-if="!$apollo.loading && categories.length >= 0"
      >
        <div
          class="shadow-sm p-2 antialiased rounded-md flex flex-col align-between justify-center category-product-card"
          v-for="product in categories[0].products"
          v-bind:key="product.id"
        >
          <img
            :src="product.imageGallery.thumb"
            class="category-product-thumb"
          />
          <span class="font-medium">{{ product.title }}</span>
          <price class="text-xl font-semibold mt-2 mb-2"
            >{{ product.price.price }}{{ product.price.currency.sign }}</price
          >
          <div class="flex items-center justify-between">
            <button class="button--grey shadow-sm">Add to cart</button>
            <div class="flex flex-row">
              <a href="#" class="text-gray-800 p-2 hover:shadow-md rounded-md">
                <svg
                  xmlns="http://www.w3.org/2000/svg"
                  width="16"
                  height="16"
                  fill="currentColor"
                  class="bi bi-heart-fill"
                  viewBox="0 0 16 16"
                >
                  <path
                    fill-rule="evenodd"
                    d="M8 1.314C12.438-3.248 23.534 4.735 8 15-7.534 4.736 3.562-3.248 8 1.314z"
                  />
                </svg>
              </a>
              <a href="#" class="text-gray-800 p-2 hover:shadow-md rounded-md">
                <svg
                  xmlns="http://www.w3.org/2000/svg"
                  width="16"
                  height="16"
                  fill="currentColor"
                  class="bi bi-arrow-left-right"
                  viewBox="0 0 16 16"
                >
                  <path
                    fill-rule="evenodd"
                    d="M1 11.5a.5.5 0 0 0 .5.5h11.793l-3.147 3.146a.5.5 0 0 0 .708.708l4-4a.5.5 0 0 0 0-.708l-4-4a.5.5 0 0 0-.708.708L13.293 11H1.5a.5.5 0 0 0-.5.5zm14-7a.5.5 0 0 1-.5.5H2.707l3.147 3.146a.5.5 0 1 1-.708.708l-4-4a.5.5 0 0 1 0-.708l4-4a.5.5 0 1 1 .708.708L2.707 4H14.5a.5.5 0 0 1 .5.5z"
                  />
                </svg>
              </a>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
const CATEGORY_PRODUCTS = require('../../../apollo/queries/categories/category_products.gql')

export default {
  name: 'Subategory',
  apollo: {
    categories: {
      query: CATEGORY_PRODUCTS,
      variables() {
        return {
          category: this.$route.params.subcategory,
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
  height: auto;
  display: flex;
  flex-direction: column;
  justify-content: start;
  align-items: center;
  text-align: center;
}

.category-product-card {
  height: auto;
}

.category-product-thumb {
  height: 15rem;
  object-fit: contain;
  width: 100%;
}
</style>
