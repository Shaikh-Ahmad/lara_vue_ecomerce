<template>
  <section>
    <!-- <h2>Hello</h2>
    <div v-for="item in cart" :key="item.id">
        <p v-text="item.name"></p>
        <p v-text="item.quantity"></p>
        <p v-text="item.price"></p>
    </div> -->
    <div>
      <h3>This is the check out</h3>
        <table class="table table-striped">
        <thead>
          <tr>
            <th scope="col">Item</th>
            <th scope="col">Quantity</th>
            <th scope="col">Price</th>
            <th scope="col">Actions</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="item in cart" :key="item.id">
            <td v-text="item.name"></td>
            <td v-text="item.quantity"></td>
            <td v-text="cartLineTotal(item)"></td>
            <td> 
              <button @click="$store.commit('removeFromCart', item)" >Remove</button>
            </td>
          </tr>
          <tr>
            <td>Total Ammount</td>
            <td v-text="cartQuantity"></td>
            <td v-text="cartTotal"></td>
          </tr>
        </tbody>
      </table>
    </div>
  </section>
</template>

<script>
export default {
  data(){
    return{
      customer:{
        first_name: '',
        last_name: '',
        email: '',
        city: '',
        state: '',
        zipcode: ''
      }
    }
  },
  methods:{
    cartLineTotal(item){
      let price =  (item.price * item.quantity);
      price = (price / 100);
      return price.toLocaleString('en-US' , {style : 'currency' , currency:'USD' })
    }
  },
  computed:{
    cart(){
      return this.$store.state.cart;
    },
    cartQuantity(){
      return this.cart.reduce((acc , item) => acc + item.quantity , 0)
    },
    cartTotal(){
      let price = this.cart.reduce((acc , item) => acc + (item.price * item.quantity), 0);
      price = (price / 100);
      return price.toLocaleString('en-US' , {style : 'currency' , currency:'USD' })
    }
  }
}
</script>

