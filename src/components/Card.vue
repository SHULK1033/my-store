<template>
  <div>
    <div class="row no-gutters mt-4">
      <div
        style="display: flex"
        class="col-md-3 my-2"
        v-for="product in displayProducts"
        :key="product.id"
      >
        <div class="card mx-auto" style="width: 20rem;">
          <img v-bind:src="product.image" class="card-img" v-bind:alt="'img ' + product.title" />
          <div class="card-body">
            <h5 class="card-title">{{ product.title }}</h5>
            <p class="card-text">{{ product.description }}</p>
          </div>
          <div class="card-footer d-flex align-items-center justify-content-between">
            <button class="btn btn-primary" type="button" @click="addCart(product)">add cart</button>
            <span>${{ formatPrice(product.price) }}</span>
          </div>
        </div>
      </div>
    </div>

    <div class="row no-gutters my-3">
      <div class="btn-group col-md-2 mx-auto">
        <button v-if="page != 1" type="button" @click="page--" class="btn btn-outline-primary">
          <i class="fas fa-backward"></i>
        </button>
        <button
          type="button"
          v-for="pageNumber in pages"
          :key="pageNumber"
          @click="page = pageNumber"
          class="btn btn-outline-primary"
        >{{ pageNumber }}</button>
        <button
          v-if="page < pages.length"
          type="button"
          @click="page++"
          class="btn btn-outline-primary"
        >
          <i class="fas fa-forward"></i>
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      //pagina actual
      page: 1,
      // items por pagina
      perPage: 8,
      // arreglo inicializado
      pages: [],
      products: [
        {
          id: "0",
          title: "Brown eggs",
          type: "dairy",
          description: "Raw organic brown eggs in a basket",
          image: "//picsum.photos/id/0/300/200",
          height: 600,
          width: 400,
          price: 28.1,
          rating: 4,
        },
        {
          id: "1",
          title: "Sweet fresh stawberry",
          type: "fruit",
          description: "Sweet fresh stawberry on the wooden table",
          image: "//picsum.photos/id/1/300/200",
          height: 450,
          width: 299,
          price: 29.45,
          rating: 4,
        },
        {
          id: "2",
          title: "Asparagus",
          type: "vegetable",
          description: "Asparagus with ham on the wooden table",
          image: "//picsum.photos/id/2/300/200",
          height: 450,
          width: 299,
          price: 18.95,
          rating: 3,
        },
        {
          id: "3",
          title: "Green smoothie",
          type: "dairy",
          description:
            "Glass of green smoothie with quail egg's yolk, served with cocktail tube, green apple and baby spinach leaves over tin surface.",
          image: "//picsum.photos/id/3/300/200",
          height: 600,
          width: 399,
          price: 17.68,
          rating: 4,
        },
        {
          id: "4",
          title: "Raw legums",
          type: "vegetable",
          description: "Raw legums on the wooden table",
          image: "//picsum.photos/id/4/300/200",
          height: 450,
          width: 299,
          price: 17.11,
          rating: 2,
        },
        {
          id: "5",
          title: "Baking cake",
          type: "dairy",
          description:
            "Baking cake in rural kitchen - dough  recipe ingredients (eggs, flour, sugar) on vintage wooden table from above.",
          image: "//picsum.photos/id/5/300/200",
          height: 450,
          width: 675,
          price: 11.14,
          rating: 4,
        },
        {
          id: "6",
          title: "Pesto with basil",
          type: "vegetable",
          description: "Italian traditional pesto with basil, chesse and oil",
          image: "//picsum.photos/id/6/300/200",
          height: 450,
          width: 299,
          price: 18.19,
          rating: 2,
        },
        {
          id: "7",
          title: "Hazelnut in black ceramic bowl",
          type: "vegetable",
          description:
            "Hazelnut in black ceramic bowl on old wooden background. forest wealth. rustic style. selective focus",
          image: "//picsum.photos/id/7/300/200",
          height: 450,
          width: 301,
          price: 27.35,
          rating: 0,
        },
        {
          id: "8",
          title: "Fresh stawberry",
          type: "fruit",
          description: "Sweet fresh stawberry on the wooden table",
          image: "//picsum.photos/id/8/300/200",
          height: 600,
          width: 399,
          price: 28.59,
          rating: 4,
        },
        {
          id: "9",
          title: "Lemon and salt",
          type: "fruit",
          description: "Rosemary, lemon and salt on the table",
          image: "//picsum.photos/id/9/300/200",
          height: 450,
          width: 299,
          price: 15.79,
          rating: 5,
        },
        {
          id: "10",
          title: "Homemade bread",
          type: "bakery",
          description: "Homemade bread",
          image: "//picsum.photos/id/10/300/200",
          height: 450,
          width: 301,
          price: 17.48,
          rating: 3,
        },
        {
          id: "11",
          title: "Legums",
          type: "vegetable",
          description: "Cooked legums on the wooden table",
          image: "//picsum.photos/id/11/300/200",
          height: 600,
          width: 399,
          price: 14.77,
          rating: 0,
        },
        {
          id: "12",
          title: "Fresh tomato",
          type: "vegetable",
          description: "Fresh tomato juice with basil",
          image: "//picsum.photos/id/12/300/200",
          height: 600,
          width: 903,
          price: 16.3,
          rating: 2,
        },
        {
          id: "13",
          title: "Healthy breakfast",
          type: "fruit",
          description:
            "Healthy breakfast set. rice cereal or porridge with berries and honey over rustic wood background",
          image: "//picsum.photos/id/13/300/200",
          height: 450,
          width: 350,
          price: 13.02,
          rating: 2,
        },
        {
          id: "14",
          title: "Green beans",
          type: "vegetable",
          description: "Raw organic green beans ready to eat",
          image: "//picsum.photos/id/14/300/200",
          height: 450,
          width: 300,
          price: 28.79,
          rating: 1,
        },
        {
          id: "15",
          title: "Baked stuffed portabello mushrooms",
          type: "bakery",
          description:
            "Homemade baked stuffed portabello mushrooms with spinach and cheese",
          image: "//picsum.photos/id/15/300/200",
          height: 600,
          width: 400,
          price: 20.31,
          rating: 1,
        },
        {
          id: "16",
          title: "Strawberry jelly",
          type: "fruit",
          description: "Homemade organic strawberry jelly in a jar",
          image: "//picsum.photos/id/16/300/200",
          height: 400,
          width: 600,
          price: 14.18,
          rating: 1,
        },
        {
          id: "17",
          title: "Pears juice",
          type: "fruit",
          description: "Fresh pears juice on the wooden table",
          image: "//picsum.photos/id/17/300/200",
          height: 600,
          width: 398,
          price: 19.49,
          rating: 4,
        },
        {
          id: "18",
          title: "Fresh pears",
          type: "fruit",
          description: "Sweet fresh pears on the wooden table",
          image: "//picsum.photos/id/18/300/200",
          height: 600,
          width: 398,
          price: 15.12,
          rating: 5,
        },
        {
          id: "19",
          title: "Caprese salad",
          type: "vegetable",
          description:
            "Homemade healthyse salad with tomato mozzarella and basil",
          image: "//picsum.photos/id/19/300/200",
          height: 400,
          width: 600,
          price: 16.76,
          rating: 5,
        },
        {
          id: "20",
          title: "Oranges",
          type: "fruit",
          description:
            "Orange popsicle ice cream bars made from fresh oranges.  a refreshing summer treat.",
          image: "//picsum.photos/id/20/300/200",
          height: 450,
          width: 274,
          price: 21.48,
          rating: 4,
        },
        {
          id: "21",
          title: "Vegan food",
          type: "vegetable",
          description: "Concept of vegan food",
          image: "//picsum.photos/id/21/300/200",
          height: 450,
          width: 299,
          price: 29.66,
          rating: 4,
        },
        {
          id: "22",
          title: "Breakfast with muesli",
          type: "dairy",
          description: "Concept of healthy breakfast with muesli",
          image: "//picsum.photos/id/22/300/200",
          height: 450,
          width: 299,
          price: 22.7,
          rating: 2,
        },
        {
          id: "23",
          title: "Honey",
          type: "bakery",
          description: "Honey and honeycell on the table",
          image: "//picsum.photos/id/23/300/200",
          height: 450,
          width: 299,
          price: 17.01,
          rating: 2,
        },
        {
          id: "24",
          title: "Breakfast with cottage",
          type: "fruit",
          description: "Healthy breakfast with cottage cheese and strawberry",
          image: "//picsum.photos/id/24/300/200",
          height: 600,
          width: 398,
          price: 14.05,
          rating: 1,
        },
        {
          image: "//picsum.photos/id/25/300/200",
          id: "25",
          type: "fruit",
          description:
            "Glass of red strawberry smoothie with chia seeds, served with retro cocktail tube, fresh mint and strawberries over dark background",
          title: "Strawberry smoothie",
          height: 600,
          width: 400,
          price: 28.86,
          rating: 2,
        },
        {
          id: "26",
          title: "Strawberry and mint",
          type: "fruit",
          description: "Homemade muesli with strawberry and mint",
          image: "//picsum.photos/id/26/300/200",
          height: 450,
          width: 299,
          price: 26.21,
          rating: 4,
        },
        {
          id: "27",
          title: "Ricotta",
          type: "dairy",
          description: "Ricotta with berry and mint",
          image: "//picsum.photos/id/27/300/200",
          height: 600,
          width: 398,
          price: 27.81,
          rating: 5,
        },
        {
          id: "28",
          title: "Cuban sandwiche",
          type: "bakery",
          description:
            "Homemade traditional cuban sandwiches with ham pork and cheese",
          image: "//picsum.photos/id/28/300/200",
          height: 450,
          width: 300,
          price: 18.5,
          rating: 4,
        },
        {
          id: "29",
          title: "Granola",
          type: "dairy",
          description:
            "Glass jar with homemade granola and yogurt with nuts, raspberries and blackberries on wooden cutting board over white textile in day light",
          image: "//picsum.photos/id/29/300/200",
          height: 450,
          width: 300,
          price: 29.97,
          rating: 3,
        },
        {
          id: "30",
          title: "Smoothie with chia seeds",
          type: "fruit",
          description:
            "Glass of red strawberry smoothie with chia seeds, served with retro cocktail tube, fresh mint and strawberries over wooden table",
          image: "//picsum.photos/id/30/300/200",
          height: 600,
          width: 900,
          price: 25.26,
          rating: 5,
        },
        {
          id: "31",
          title: "Yogurt",
          type: "dairy",
          description: "Homemade yogurt with raspberry and mint",
          image: "//picsum.photos/id/31/300/200",
          height: 450,
          width: 299,
          price: 27.61,
          rating: 4,
        },
        {
          id: "32",
          title: "Sandwich with salad",
          type: "vegetable",
          description: "Vegan sandwich with salad, tomato and radish",
          image: "//picsum.photos/id/32/300/200",
          height: 600,
          width: 398,
          price: 22.48,
          rating: 5,
        },
        {
          id: "33",
          title: "Cherry",
          type: "fruit",
          description: "Cherry with sugar on old table",
          image: "//picsum.photos/id/33/300/200",
          height: 600,
          width: 400,
          price: 14.35,
          rating: 5,
        },
        {
          id: "34",
          title: "Raw asparagus",
          type: "vegetable",
          description: "Raw fresh asparagus salad with cheese and dressing",
          image: "//picsum.photos/id/34/300/200",
          height: 600,
          width: 400,
          price: 22.97,
          rating: 4,
        },
        {
          id: "35",
          title: "Corn",
          type: "vegetable",
          description: "Grilled corn on the cob with salt and butter",
          image: "//picsum.photos/id/35/300/200",
          height: 450,
          width: 300,
          price: 13.55,
          rating: 2,
        },
        {
          id: "36",
          title: "Vegan",
          type: "vegan",
          description: "Concept of healthy vegan eating",
          image: "//picsum.photos/id/36/300/200",
          height: 600,
          width: 398,
          price: 28.96,
          rating: 5,
        },
        {
          id: "37",
          title: "Fresh blueberries",
          type: "fruit",
          description:
            "Healthy breakfast. berry crumble with fresh blueberries, raspberries, strawberries, almond, walnuts, pecans, yogurt, and mint in ceramic plates over white wooden surface, top view",
          image: "//picsum.photos/id/37/300/200",
          height: 450,
          width: 321,
          price: 21.01,
          rating: 4,
        },
        {
          id: "38",
          title: "Smashed avocado",
          type: "fruit",
          description:
            "Vegan sandwiches with smashed avocado, tomatoes and radish. top view",
          image: "//picsum.photos/id/38/300/200",
          height: 450,
          width: 450,
          price: 25.88,
          rating: 0,
        },
        {
          id: "39",
          title: "Italian ciabatta",
          type: "bakery",
          description:
            "Italian ciabatta bread cut in slices on wooden chopping board with herbs, garlic and olives over dark grunge backdrop, top view",
          image: "//picsum.photos/id/39/300/200",
          height: 450,
          width: 565,
          price: 15.18,
          rating: 1,
        },
        {
          id: "40",
          title: "Rustic breakfast",
          type: "dairy",
          description:
            "Rustic healthy breakfast set. cooked buckwheat groats with milk and honey on dark grunge backdrop. top view, copy space",
          image: "//picsum.photos/id/40/300/200",
          height: 450,
          width: 307,
          price: 21.32,
          rating: 0,
        },
        {
          id: "41",
          title: "Sliced lemons",
          type: "fruit",
          description:
            "Heap of whole and sliced lemons and limes with mint in vintage metal grid box over old wooden table with turquoise wooden background. dark rustic style.",
          image: "//picsum.photos/id/41/300/200",
          height: 600,
          width: 900,
          price: 27.14,
          rating: 2,
        },
        {
          id: "42",
          title: "Plums",
          type: "fruit",
          description: "Yellow and red sweet plums",
          image: "//picsum.photos/id/42/300/200",
          height: 450,
          width: 299,
          price: 19.18,
          rating: 1,
        },
        {
          id: "43",
          title: "French fries",
          type: "bakery",
          description: "Homemade oven baked french fries with ketchup",
          image: "//picsum.photos/id/43/300/200",
          height: 600,
          width: 400,
          price: 18.32,
          rating: 3,
        },
        {
          id: "44",
          title: "Strawberries",
          type: "fruit",
          description:
            "Healthy breakfast set. rice cereal or porridge with fresh strawberry, apricots, almond and honey over white rustic wood backdrop, top view, \u0000",
          image: "//picsum.photos/id/44/300/200",
          height: 450,
          width: 352,
          price: 15.13,
          rating: 3,
        },
        {
          id: "45",
          title: "Ground beef meat burger",
          type: "meat",
          description:
            "Raw ground beef meat burger steak cutlets with seasoning on vintage wooden boards, black background",
          image: "//picsum.photos/id/45/300/200",
          height: 450,
          width: 675,
          price: 11.73,
          rating: 5,
        },
        {
          id: "46",
          title: "Tomatoes",
          type: "fruit",
          description: "Organic tomatoes made with love",
          image: "//picsum.photos/id/46/300/200",
          height: 450,
          width: 675,
          price: 26.03,
          rating: 4,
        },
        {
          id: "47",
          title: "Basil",
          type: "vegetable",
          description: "Concept of vegan food with basil",
          image: "//picsum.photos/id/47/300/200",
          height: 450,
          width: 678,
          price: 15.19,
          rating: 4,
        },
        {
          id: "48",
          title: "Fruits bouquet",
          type: "fruit",
          description: "Abstract citrus fruits bouquet on blue background",
          image: "//picsum.photos/id/48/300/200",
          height: 600,
          width: 401,
          price: 18.18,
          rating: 1,
        },
        {
          id: "49",
          title: "Peaches on branch",
          type: "fruit",
          description:
            "Peaches on branch with leaves and glasses with peach juice and limonade with ice cubes in aluminum tray over old metal table. dark rustic style. top view.",
          image: "//picsum.photos/id/49/300/200",
          height: 600,
          width: 400,
          price: 25.62,
          rating: 3,
        },
      ],
    };
  },

  methods: {
    // da formato al precio
    formatPrice(value) {
      let val = (value / 1).toFixed(2).replace(".", ",");
      return val.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ".");
    },
    // calcula la cantidad de paginas requeridas segun la cantidad de datos totales y la cantidad que se mostrara en pantalla
    paginate(products) {
      let page = this.page;
      let perPage = this.perPage;

      let from = page * perPage - perPage;
      let to = page * perPage;

      return products.slice(from, to);
    },
    // paginacion de productos
    setProducts() {
      let numberOfPages = Math.ceil(this.products.length / this.perPage);
      for (let i = 1; i <= numberOfPages; i++) {
        this.pages.push(i);
      }
    },
    // envia el objeto al componente padre
    addCart(product) {
      this.$emit("product", product);
    },
  },
  // computar objetos para monipulacion
  computed: {
    displayProducts() {
      return this.paginate(this.products);
    },
  },
  // implementacion de paginacion
  created() {
    this.setProducts();
  },
};
</script>

<style>
</style>
