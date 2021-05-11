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

Create environment variables

```sh
$ sudo nano .env
```
Example environment variables
```sh
VUE_APP_GRAPHQL_HTTP=http://oxidshop.com/graphql?skipSession=1
VUE_APP_GRAPHQL_WS=ws://oxidshop.com/graphql?skipSession=1
```

Run development server
```sh
$ npm run dev
```
