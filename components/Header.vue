<template>
  <nav class="bg-gray-800">
    <div class="max-w-7xl mx-auto px-2 sm:px-6 lg:px-8">
      <div class="relative flex items-center justify-between h-16">
        <div class="absolute inset-y-0 left-0 flex items-center sm:hidden">
          <!-- Mobile menu button-->
          <button
            type="button"
            class="inline-flex items-center justify-center p-2 rounded-md text-gray-400 hover:text-white hover:bg-gray-700 focus:outline-none focus:ring-2 focus:ring-inset focus:ring-white"
            aria-controls="mobile-menu"
            aria-expanded="false"
          >
            <span class="sr-only">Open main menu</span>
            <!--
              Icon when menu is closed.

              Heroicon name: outline/menu

              Menu open: "hidden", Menu closed: "block"
            -->
            <svg
              class="block h-6 w-6"
              xmlns="http://www.w3.org/2000/svg"
              fill="none"
              viewBox="0 0 24 24"
              stroke="currentColor"
              aria-hidden="true"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                d="M4 6h16M4 12h16M4 18h16"
              />
            </svg>
            <!--
              Icon when menu is open.

              Heroicon name: outline/x

              Menu open: "block", Menu closed: "hidden"
            -->
            <svg
              class="hidden h-6 w-6"
              xmlns="http://www.w3.org/2000/svg"
              fill="none"
              viewBox="0 0 24 24"
              stroke="currentColor"
              aria-hidden="true"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                d="M6 18L18 6M6 6l12 12"
              />
            </svg>
          </button>
        </div>
        <div
          class="flex-1 flex items-center justify-center sm:items-stretch sm:justify-start"
        >
          <div class="flex-shrink-0 flex items-center">
            <img
              class="block lg:hidden h-10 w-auto"
              src="../assets/logo.png"
              alt="Workflow"
            />
            <img
              class="hidden lg:block h-10 w-auto"
              src="../assets/logo.png"
              alt="Workflow"
            />
          </div>
          <div class="hidden sm:block sm:ml-6">
            <div class="flex space-x-4" v-if="!$apollo.loading && categoryTree">
              <div
                class="group relative inline-block text-left"
                v-for="category in categoryTree"
                v-bind:key="category.id"
              >
                <div>
                  <a
                    class="inline-flex justify-center w-full text-gray-300 hover:bg-gray-700 hover:text-white px-3 py-2 rounded-md text-sm font-medium"
                    id="menu-button"
                    aria-expanded="true"
                    aria-haspopup="true"
                    @click="routeCategory(category.title)"
                  >
                    <!-- :to="category.title" -->
                    {{ category.title }}

                    <svg
                      v-if="Object.keys(category.children).length > 0"
                      class="-mr-1 ml-2 h-5 w-5"
                      xmlns="http://www.w3.org/2000/svg"
                      viewBox="0 0 20 20"
                      fill="currentColor"
                      aria-hidden="true"
                    >
                      <path
                        fill-rule="evenodd"
                        d="M5.293 7.293a1 1 0 011.414 0L10 10.586l3.293-3.293a1 1 0 111.414 1.414l-4 4a1 1 0 01-1.414 0l-4-4a1 1 0 010-1.414z"
                        clip-rule="evenodd"
                      />
                    </svg>
                  </a>
                </div>

                <div
                  v-if="Object.keys(category.children).length > 0"
                  class="menu-bottom origin-top-left absolute left-0 w-56 rounded-md shadow-lg bg-white ring-1 ring-black ring-opacity-5 focus:outline-none"
                  role="menu"
                  aria-orientation="vertical"
                  aria-labelledby="menu-button"
                  tabindex="-1"
                >
                  <div class="py-1" role="none">
                    <!-- Active: "bg-gray-100 text-gray-900", Not Active: "text-gray-700" -->
                    <a
                      v-for="children in category.children"
                      v-bind:key="children.id"
                      class="text-gray-700 block px-4 py-2 text-sm hover:bg-gray-100"
                      role="menuitem"
                      tabindex="-1"
                      id="menu-item-0"
                      @click="routeSubcategory(category.title, children.title)"
                      >{{ children.title }}</a
                    >
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
        <div
          class="absolute inset-y-0 right-0 flex items-center pr-2 sm:static sm:inset-auto sm:ml-6 sm:pr-0"
        >
          <button
            class="bg-gray-800 p-1 rounded-full text-gray-400 hover:text-white focus:outline-none"
          >
            <span class="sr-only">View notifications</span>
            <!-- Heroicon name: outline/bell -->
            <svg
              xmlns="http://www.w3.org/2000/svg"
              width="26"
              height="26"
              fill="currentColor"
              class="bi bi-cart2"
              viewBox="0 0 16 16"
            >
              <path
                d="M0 2.5A.5.5 0 0 1 .5 2H2a.5.5 0 0 1 .485.379L2.89 4H14.5a.5.5 0 0 1 .485.621l-1.5 6A.5.5 0 0 1 13 11H4a.5.5 0 0 1-.485-.379L1.61 3H.5a.5.5 0 0 1-.5-.5zM3.14 5l1.25 5h8.22l1.25-5H3.14zM5 13a1 1 0 1 0 0 2 1 1 0 0 0 0-2zm-2 1a2 2 0 1 1 4 0 2 2 0 0 1-4 0zm9-1a1 1 0 1 0 0 2 1 1 0 0 0 0-2zm-2 1a2 2 0 1 1 4 0 2 2 0 0 1-4 0z"
              />
            </svg>
          </button>
        </div>
      </div>
    </div>

    <!-- Mobile menu, show/hide based on menu state. -->
    <div class="sm:hidden" id="mobile-menu">
      <div class="px-2 pt-2 pb-3 space-y-1">
        <!-- Current: "bg-gray-900 text-white", Default: "text-gray-300 hover:bg-gray-700 hover:text-white" -->
        <a
          href="#"
          class="bg-gray-900 text-white block px-3 py-2 rounded-md text-base font-medium"
          aria-current="page"
          >Dashboard</a
        >

        <a
          href="#"
          class="text-gray-300 hover:bg-gray-700 hover:text-white block px-3 py-2 rounded-md text-base font-medium"
          >Team</a
        >

        <a
          href="#"
          class="text-gray-300 hover:bg-gray-700 hover:text-white block px-3 py-2 rounded-md text-base font-medium"
          >Projects</a
        >

        <a
          href="#"
          class="text-gray-300 hover:bg-gray-700 hover:text-white block px-3 py-2 rounded-md text-base font-medium"
          >Calendar</a
        >
      </div>
    </div>
  </nav>
</template>

<script>
const ALL_CATEGORIES = require('../apollo/queries/categories/all_categories.gql')

export default {
  apollo: {
    categories: {
      query: ALL_CATEGORIES,
      result(data) {
        return this.setCategories(data)
      },
    },
  },
  data() {
    return {
      categoryTree: [],
    }
  },
  methods: {
    setCategories(data) {
      console.log(data)
      const categoryTree = []
      const rootCategories = []
      data.data.categories.forEach((item) => {
        // First off, set root categories
        if (item.root && !rootCategories.includes(item.root.id)) {
          rootCategories.push(item.root.id)
          const children = data.data.categories.filter((c) => {
            const parent = c.parent ? c.parent.id : null
            if (parent) {
              return parent === item.root.id
            }
            return parent
          })
          categoryTree.push({
            id: item.root.id,
            title: item.root.title,
            url: item.seo.url,
            children: {
              ...children.map((x) => ({
                id: x.id,
                title: x.title,
                url: x.seo.url,
              })),
            },
          })
        }
      })
      this.categoryTree = categoryTree
    },
    routeCategory(category) {
      this.$router.push({
        name: 'categories-category',
        params: {
          category,
        },
      })
    },
    routeSubcategory(category, subcategory) {
      this.$router.push({
        name: 'categories-category-subcategory',
        params: {
          category,
          subcategory,
        },
      })
    },
  },
}
</script>

<style>
nav a {
  cursor: pointer;
}

.menu-bottom {
  display: none;
}

.menu-bottom:hover {
  display: block;
}

.group:hover .menu-bottom {
  display: block;
}
</style>
