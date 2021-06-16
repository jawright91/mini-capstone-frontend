<template>
  <div class="home">
    <div class="row">
      <div class="col-sm-4" v-for="product in products" v-bind:key="product.id">
        <div class="card">
          <div class="carousel-inner">
            <div class="carousel-item active" v-for="image in product.images" v-bind:key="image.id">
              <img class="d-block w-100" v-bind:src="image.url" v-bind:alt="product.title" />
            </div>
          </div>
          <a class="carousel-control-prev" href="#carouselExampleControls" role="button" data-slide="prev">
            <span class="carousel-control-prev-icon" aria-hidden="true"></span>
            <span class="sr-only">Previous</span>
          </a>
          <a class="carousel-control-next" href="#carouselExampleControls" role="button" data-slide="next">
            <span class="carousel-control-next-icon" aria-hidden="true"></span>
            <span class="sr-only">Next</span>
          </a>
        </div>
        <div class="card-body">
          <h2 class="card-title">{{ product.name }}</h2>
          <p class="card-text">$ {{ product.price }}</p>
          <button
            type="button"
            class="btn btn-primary"
            data-toggle="modal"
            data-target="#active-product"
            v-on:click="setActiveProduct(product)"
          >
            More info
          </button>
        </div>
      </div>

      <!-- Modal -->
      <div
        class="modal fade"
        id="active-product"
        tabindex="-1"
        role="dialog"
        aria-labelledby="exampleModalCenterTitle"
        aria-hidden="true"
      >
        <div class="modal-dialog modal-dialog-centered" role="document">
          <div class="modal-content">
            <div class="modal-header">
              <h5 class="modal-title" id="exampleModalLongTitle">{{ activeProduct.name }}</h5>
              <button type="button" class="close" data-dismiss="modal" aria-label="Close">
                <span aria-hidden="true">&times;</span>
              </button>
            </div>
            <div class="modal-body">...</div>
            <div class="modal-footer">
              <button type="button" class="btn btn-secondary" data-dismiss="modal">Close</button>
              <button type="button" class="btn btn-primary">Save changes</button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>

  <!-- <div v-for="recipe in recipes" v-bind:key="recipe.id">
      <h2>{{ recipe.title }}</h2>
      <p>by {{ recipe.chef }}</p>
      <a v-bind:href="`/recipes/${recipe.id}`">More info</a>
    </div> -->
  <!-- </div> -->

  <!-- <div v-for="product in products" v-bind:key="product.id">
      <h1>{{ product.name }}</h1>
      <div id="carouselExampleControls" class="carousel slide" data-ride="carousel">
 
    </div> -->
  <!-- </div> -->
</template>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      products: ["hello"],
      activeProduct: ["If you can see this, something is borked"],
    };
  },
  created: function () {
    this.loadProducts();
  },
  methods: {
    loadProducts: function () {
      axios.get("/products/").then((response) => {
        console.log("poop", response.data);
        this.products = response.data;
      });
    },
    setActiveProduct: function (product) {
      this.activeProduct = product;
      console.log(this.activeProduct);
    },
  },
};
</script>
