<template>
  <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
    <a class="navbar-brand" href="#">My Store</a>
    <button
      class="navbar-toggler"
      type="button"
      data-toggle="collapse"
      data-target="#navbarNavDropdown"
      aria-controls="navbarNavDropdown"
      aria-expanded="false"
      aria-label="Toggle navigation"
    >
      <span class="navbar-toggler-icon"></span>
    </button>
    <div class="collapse navbar-collapse" id="navbarNavDropdown">
      <ul class="navbar-nav">
        <li v-for="item in items" :key="item.route" class="nav-item">
          <a class="nav-link" v-bind:href="item.route">{{ item.name }}</a>
        </li>
      </ul>
      <ul class="navbar-nav ml-auto">
        <li class="nav-item">
          <a href class="btn btn-secondary text-white">
            <i class="fas fa-shopping-cart"></i> 0
          </a>
        </li>
      </ul>
    </div>
  </nav>
</template>

<script>
export default {
  data() {
    return {
      items: [
        {
          route: "/",
          name: "Home",
        },
        {
          route: "/store",
          name: "Teinda",
        },
      ],
    };
  },
};
</script>

<style>
</style>