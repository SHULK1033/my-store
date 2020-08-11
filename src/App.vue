<template>
  <div id="app">
    <!-- la navbar recive la cantidad de productos agregados -->
    <Navbar :cart="products.length" />
    <!-- las tarjetas son los productos disponibles y envian al padre el evento que lleva el producto al modal -->
    <Card @product="addNavbar($event)" />

    <!-- Modal que mostrara los productos agregador al carro -->
    <div
      class="modal fade"
      id="exampleModalCenter"
      tabindex="-1"
      role="dialog"
      aria-labelledby="exampleModalCenterTitle"
      aria-hidden="true"
    >
      <div
        class="modal-dialog modal-lg modal-dialog-centered modal-dialog-scrollable"
        role="document"
      >
        <div class="modal-content">
          <div class="modal-header">
            <h5 class="modal-title" id="exampleModalLongTitle">My Cart: {{ products.length }}</h5>
            <button type="button" class="close" data-dismiss="modal" aria-label="Close">
              <span aria-hidden="true">&times;</span>
            </button>
          </div>
          <div class="modal-body">
            <div class="row align-items-center my-5 text-center" v-for="(product, index) in products" :key="index">
              <div class="col-md-3">
                <img :src="product.image" :alt="product.title" class="img-fluid" />
              </div>
              <div class="col-md-3">{{ product.title }}</div>
              <div class="col-md-3">$ {{ formatPrice(product.price) }}</div>
              <div class="col-md-3">
                <button class="btn btn-danger" type="button" @click="deleteProduct(index)">
                  <i class="fas fa-trash-alt"></i>
                </button>
              </div>
            </div>
          </div>
          <div class="modal-footer justify-content-start">
            <button type="button" class="btn btn-secondary" data-dismiss="modal">Close</button>
            <button type="button" class="btn btn-primary">Checkout</button>
            <span class="ml-auto pr-2">Total: $ {{ formatPrice(checkout(total)) }}</span>
          </div>
        </div>
      </div>
    </div>
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
      total: 0,
    };
  },
  methods: {
    // agrega la cantidad de items al carrito
    addNavbar(product) {
      this.products.push(product);
      return product;
    },
    // borra el prodcuto seleccionado por el indice
    deleteProduct(productIndex) {
      for (let i = 0; i < this.products.length; i++) {
        if (i === productIndex) {
          this.products.splice(i, 1);
        }
      }
    },
    // calcula el valor total de los productos agregados
    checkout(total) {
      for (let i = 0; i < this.products.length; i++) {
        total += this.products[i].price;
      }
      return total;
    },
    //da formato al precio colocando una coma como decimal y un punto indicando mil o mas
    formatPrice(value) {
      let val = (value / 1).toFixed(2).replace(".", ",");
      return val.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ".");
    },
  },
};
</script>

<style>
</style>
