<template>
  <div id="app">
    <Navbar />
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
};
</script>

<style>
</style>
