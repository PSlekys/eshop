<template>
  <div class="products">
    <h2 class="subtitle">Products</h2>

    <Search v-on:search="filter" />

    <div class="columns">
      <div
        class="column is-one-quarter"
        v-for="product in products"
        :key="product.id"
      >
        <Product
          :name="product.name"
          :image="product.image"
          :description="product.description"
          :price="product.price"
        />
      </div>
    </div>
  </div>
</template>

<script>
import firebase from "firebase/app";
import "firebase/firestore";
import Product from "../components/Product";
import Search from "../components/Search";

export default {
  name: "Products",
  components: { Product, Search },
  data() {
    return {
      allproducts: [],
      products: [],
    };
  },
  methods: {
    filter(query) {
      this.products = this.allproducts.filter((product) =>
        product.name.toLowerCase().includes(query.toLowerCase())
      );
    },
  },
  beforeMount() {
    firebase
      .firestore()
      .collection("products")
      .get()
      .then((snapshot) =>
        snapshot.docs.forEach((doc) => {
          this.allproducts.push({
            id: doc.id,
            image: doc.data().image,
            name: doc.data().name,
            description: doc.data().description,
            price: doc.data().price,
          });
          this.products = this.allproducts;
        })
      );
  },
};
</script>
