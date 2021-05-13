<template>
  <div>
    <div class="h-10 w-full bg-gray-100 flex items-center justify-start pl-5">
      <div
        class="max-w-7xl mx-auto px-2 sm:px-6 lg:px-8 font-medium text-gray-400"
      ></div>
    </div>
    <div class="max-w-7xl mx-auto px-2 sm:px-6 lg:px-8 mt-6">
      <div
        class="flex align-center flex-col sm:flex-row justify-between"
        v-if="!$apollo.loading && product"
      >
        <div
          class="text-left sm:w-2/3 w-auto flex flex-col product-image-wrapper"
        >
          <img :src="currentImage" class="product-image object-contain" />
          <div
            class="flex flex-row mt-2 justify-center"
            v-if="product.imageGallery.images.length > 1"
          >
            <div
              class="h-24 w-24 m-2 hover:shadow-md p-2 flex justify-center cursor-pointer"
              v-for="image in product.imageGallery.images"
              v-bind:key="image.image"
              @click="setProductImage(image.zoom)"
            >
              <img class="" :src="image.image" />
            </div>
          </div>
        </div>
        <div
          class="flex sm:w-1/3 bg-gray-100 justify-start flex-col align-start p-4 mt-4 sm:mt-0"
        >
          <span class="text-2xl mb-2">{{ product.title }}</span>
          <div class="flex justify-between">
            <span class="font-medium"
              >{{ product.price.price }}{{ product.price.currency.sign }}</span
            >
            <span class="text-green-500 font-medium"
              >Available - {{ product.stock.stock }}</span
            >
          </div>

          <div class="mt-4 flex">
            <input
              class="border-0 outline-none w-1/4 p-4 text-lg font-medium"
              type="number"
              min="1"
              value="1"
            />
            <button
              class="uppercase bg-gray-800 hover:bg-gray-700 p-4 w-full text-white font-medium"
            >
              Add to cart
            </button>
          </div>

          <span class="font-bold mt-4">Description</span>
          <div>
            <span>
              {{ product.shortDescription }}
            </span>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
const SINGLE_PRODUCT = require('../../apollo/queries/products/single_product.gql')

export default {
  name: 'Product',
  apollo: {
    product: {
      query: SINGLE_PRODUCT,
      variables() {
        return {
          id: this.$route.params.id,
        }
      },
      result(data) {
        this.prepareProduct(data)
      },
    },
  },
  data() {
    return {
      currentImage: '',
    }
  },
  methods: {
    prepareProduct(data) {
      console.log(data)
      this.currentImage = data.data.product.imageGallery.images[0].zoom
    },
    setProductImage(image) {
      this.currentImage = image
    },
  },
}
</script>

<style>
.container {
  margin: 0 auto;
  height: auto;
  display: flex;
  flex-direction: column;
  justify-content: start;
  align-items: center;
  text-align: center;
}
.product-image {
  max-height: 30rem;
}
.product-image-wrapper {
  max-height: 90vh;
}
</style>
