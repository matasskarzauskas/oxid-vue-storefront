<template>
  <div class="container">
    <div
      class="bg-white shadow-md rounded px-8 pt-6 pb-8 m-8 flex flex-col login-wrapper"
    >
      <div class="mb-4">
        <label
          class="block text-grey-darker text-sm font-bold mb-2"
          for="username"
        >
          Email
        </label>
        <input
          class="shadow appearance-none border rounded w-full py-2 px-3 text-grey-darker"
          id="email"
          type="email"
          v-model="email"
          placeholder="Email"
        />
      </div>
      <div class="mb-6">
        <label
          class="block text-grey-darker text-sm font-bold mb-2"
          for="password"
        >
          Password
        </label>
        <input
          class="shadow appearance-none border border-red rounded w-full py-2 px-3 text-grey-darker mb-3"
          id="password"
          type="password"
          v-model="password"
          placeholder="******************"
        />
      </div>
      <div
        class="mb-8 text-white bg-red-500 rounded p-4 flex align-center"
        v-if="displayError"
      >
        <svg
          xmlns="http://www.w3.org/2000/svg"
          width="24"
          height="24"
          fill="currentColor"
          class="bi bi-exclamation-octagon"
          viewBox="0 0 16 16"
        >
          <path
            d="M4.54.146A.5.5 0 0 1 4.893 0h6.214a.5.5 0 0 1 .353.146l4.394 4.394a.5.5 0 0 1 .146.353v6.214a.5.5 0 0 1-.146.353l-4.394 4.394a.5.5 0 0 1-.353.146H4.893a.5.5 0 0 1-.353-.146L.146 11.46A.5.5 0 0 1 0 11.107V4.893a.5.5 0 0 1 .146-.353L4.54.146zM5.1 1 1 5.1v5.8L5.1 15h5.8l4.1-4.1V5.1L10.9 1H5.1z"
          />
          <path
            d="M7.002 11a1 1 0 1 1 2 0 1 1 0 0 1-2 0zM7.1 4.995a.905.905 0 1 1 1.8 0l-.35 3.507a.552.552 0 0 1-1.1 0L7.1 4.995z"
          />
        </svg>
        <span class="ml-4 font-bold">Entered credentials are invalid!</span>
      </div>
      <div class="flex items-center justify-between mb-4">
        <button
          class="bg-gray-800 hover:bg-gray-700 text-white font-bold py-2 px-4 rounded"
          type="button"
          @click="signIn()"
        >
          Sign In
        </button>
        <a
          class="inline-block align-baseline font-bold text-sm text-blue hover:text-blue-darker"
          href="#"
        >
          Forgot Password?
        </a>
      </div>
      <hr />
      <div class="mt-4 text-sm">
        <span
          >Don't have an account yet?
          <a href="#" class="font-bold">Create account</a></span
        >
      </div>
    </div>
  </div>
</template>

<script>
const AUTHORIZATION = require('../../apollo/queries/user/authorization.gql')

export default {
  name: 'Login',
  apollo: {
    token: {
      query: AUTHORIZATION,
      variables() {
        return {
          username: this.email,
          password: this.password,
        }
      },
      skip() {
        return this.skipQuery
      },
      result(data) {
        this.finishQuery(data)
      },
    },
  },
  data() {
    return {
      skipQuery: true,
      userLogins: null,
      email: '',
      password: '',
      displayError: false,
    }
  },
  methods: {
    signIn() {
      if (!this.email || !this.password) return

      this.skipQuery = false
      this.$apollo.queries.token.refetch()
    },
    finishQuery(data) {
      console.log(data)
      if (data.data) {
        console.log(data.data.token)
      } else {
        this.displayError = true
      }

      this.skipQuery = true
    },
  },
}
</script>

<style>
.container {
  margin: 0 auto;
  height: 100%;
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
}
.login-wrapper {
  min-width: 15rem;
  width: 30rem;
}
</style>
