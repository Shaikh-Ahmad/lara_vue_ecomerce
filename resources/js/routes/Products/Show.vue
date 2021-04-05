<template>
  <section>
    <h2>A product</h2>
      <div class="card m-2">
        <img class="rounded mx-auto d-block"  width="225x" height="200px">
      <div class="text-center">
        <p v-text="product.name"></p>
        <p v-text="formateCurrency(product.price)"></p>
        <p v-for="category in product.categories" v-text="category.name" :key="category.id"></p>
        <p v-text="product.description" class="p-4"></p>
      </div>
      <div>
        <button @click="$store.commit('addToCart', product)" >Add to cart</button> 
      </div>
    </div>
  </section>
</template>

<script>
export default {
    methods:{
      formateCurrency(price){
      price = (price / 100);
      return price.toLocaleString('en-US' , {style : 'currency' , currency:'USD' })
      }
    },
   computed: {
      products() {
        return this.$store.state.products;
      },
       product() {
        return this.products.find(product => product.slug == this.$route.params.slug);
      }
    }
}
</script>
