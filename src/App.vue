<template>
  <div id="app">
    <Navbar :cart="products.length" />
    <Card />
  </div>
</template>

<script>
import Navbar from "./components/Navbar";
import Card from "./components/Card";

export default {
  name: "App",
  components: {
    Navbar,
    Card,
  },
  data() {
    return {
      products: [],
    };
  },
};
</script>

<style>
</style>
