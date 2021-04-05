<template>
  <section>
    <div>
        <div v-if="!products.length">
          loding products....
        </div>
        <div class="row" v-else>
          <div class="col col-md-3" v-for="product in products" :key="product.id">
            <div class="card m-2">
              <router-link :to="{name: 'products.show', params: {slug: product.slug}}">
                <img class="rounded mx-auto d-block"  width="225x" height="200px">
              </router-link>
              <div class="text-center">
                <p v-text="product.name"></p>
                <p v-text="formateCurrency(product.price)"></p>
              </div>
            </div>
          </div>
        </div> 
    </div>
  </section>
</template>

<script>
  export default {
    computed: {
      products() {
        return this.$store.state.products;
      }
    },
    methods:{
      formateCurrency(price){
      price = (price / 100);
      return price.toLocaleString('en-US' , {style : 'currency' , currency:'USD' })
    }
    }
  }
</script>

