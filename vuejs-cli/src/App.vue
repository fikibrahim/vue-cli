<template>
  <div class="container mt-5">
    <h1>IDShop</h1>
    <product-list
      :products="products"
      maximum="maximum"
      @add="addItem"
    ></product-list>
    <!-- <p class="animate__animated animate__fadeInRight">
      Lorem ipsum dolor sit amet consectetur, adipisicing elit. Maxime maiores
      impedit obcaecati voluptas harum natus earum, nulla illo lgitabore rerum,
      pariatur nihil! Maxime, quae hic adipisci nam corporis eligendi placeat
      ipsum sequi necessitatibus rerum tenetur numquam delectus maiores
      distinctio in doloribus, exercitationem magni, consequatur a. Quod, alias.
      Ducimus, ad sunt.
    </p>
    <font-awesome-icon icon="shopping-cart"></font-awesome-icon>
    <Price :value="2.23" /> -->
  </div>
  <!-- <header>
    <img alt="Vue logo" class="logo" src="./assets/logo.svg" width="125" height="125" />

    <div class="wrapper">
      <HelloWorld msg="You did it!" />
    </div>
  </header>

  <main>
    <TheWelcome />
  </main> -->
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
// import TheWelcome from './components/TheWelcome.vue'
// import { FontAwesomeIcon } from "@fortawesome/vue-fontawesome";
// import Price from "./components/Price.vue";
import ProductList from "./components/ProductList.vue";

export default {
  name: "app",
  data: function () {
    return {
      maximum: 20,
      products: [],
      cart: [],
    };
  },
  components: {
    // FontAwesomeIcon,
    ProductList,
  },
  mounted: function () {
    fetch("https://hplussport.com/api/products/order/price")
      .then((response) => response.json())
      .then((data) => {
        this.products = data;
      });
  },
  methods: {
    addItem: function (product) {
      let productIndex;
      let productExist = this.cart.filter(function (item, index) {
        if (item.product.id == Number(product.id)) {
          productIndex = index;
          return true;
        } else {
          return false;
        }
      });

      if (productExist.length) {
        this.cart[this.productIndex].qty++;
      } else {
        this.cart.push({ product: product, qty: 1 });
      }
    },
  },
};
</script>

<!-- <style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style> -->
