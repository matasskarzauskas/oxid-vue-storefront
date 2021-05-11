![Oxid Storefront](https://i.ibb.co/rwRvJmS/oxid-vue-git.png)
### This project is work in progress!

## Requirements

This theme requires OXID installation to have following modules installed and enabled
| Module | Link |
| ------ | ------ |
| graphql-base-module | [https://github.com/OXID-eSales/graphql-base-module][PlGh] |
| graphql-storefront-module | [https://github.com/OXID-eSales/graphql-storefront-module][PlGd] |
   
   [PlGh]: <https://github.com/OXID-eSales/graphql-base-module>
   [PlGd]: <https://github.com/OXID-eSales/graphql-storefront-module>

## Installation

Clone github repository
```sh
$ git clone https://github.com/matasskarzauskas/oxid-vue-storefront.git
```
```sh
$ cd oxid-vue-storefront
```

Install modules
```sh
$ npm install
```

Change GraphQL endpoint in `nuxt.config.js`

Example
```sh
httpEndpoint: 'http://localhost/graphql?skipSession=1'
```

Run development server
```sh
$ npm run dev
```
