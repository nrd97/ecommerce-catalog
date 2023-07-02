<template>
  <div class="container">
    <div class="product" v-if="product">
      <div class="content">
        <div class="image">
          <img :src="product.image" />
        </div>
        <div class="text">
          <h2>{{ product.title }}</h2>
          <p>{{ product.category }}</p>
          <hr />
          <p>{{ product.description }}</p>
        </div>
      </div>
        <div class="text2">
        <hr />
        <h2 class="price">${{ product.price }}</h2>
        <div class="btn">
          <button class="btn-buy">Buy now</button>
          <button class="btn-next" @click="nextProduct">Next product</button>
        </div>
      </div>
    </div>
  </div>
</template> 
 
<script>
export default {
  data() {
    return {
      products: [],
      currentIndex: 0,
    };
  },

  mounted() {
    this.getData ();
  },
 
  methods: {
    getData() {
      fetch('https://fakestoreapi.com/products')
      .then(response => response.json())
      .then(data => {
        const filteredProducts = data.filter(product => {
          return product.category === "men's clothing" || product.category === "women's clothing";
        });
        this.products = filteredProducts;
      })
      .catch(error => {
        console.log(error);
      });
    },
    
    nextProduct() {
      this.currentIndex = (this.currentIndex + 1) % this.products.length;
    }
  },

  computed: {
    product() {
      return this.products[this.currentIndex];
    }
  },

  created() {
    this.getData();
  }
};
</script>