<template>
  <div>
    <h3>Todos.id</h3>
    <div id="app">
      <input type="text" v-model="form.name" id="txt_1" placeholder="Add Something ..." >
      <button @click="addToCart">+</button>
    </div>
    <ul>
      <li v-for="(cart, index) in carts" :key="index">
        {{ cart.name }}
        <button @click="remove(cart)">&times;</button>
      </li>
    </ul>
  </div>
</template>
<script>
import axios from 'axios'
import cookie from 'vue-cookie'
export default{
  data:()=>({
    carts:[],
    form: {
      name: ''
    },
  }),

  mounted(){
     if(localStorage.getItem('carts')) {
      try {
        this.carts = JSON.parse(localStorage.getItem('carts'));
      } catch(e) {
        localStorage.removeItem('carts');
      }
    }
  },

  methods: {
    addToCart() {
      this.carts.push({
        name: this.form.name
      })
      this.form.name = ''
      this.saveCats();
      this.saveCatsCookie();
    },

    saveCats() {
      let parsed = JSON.stringify(this.carts);
      localStorage.setItem('carts', parsed);
    },

    saveCatsCookie() {
      let parsed = JSON.stringify(this.carts);
      localStorage.setItem('carts', parsed);
      // Cookies.set("carts", JSON.stringify(this.carts), {expires: '1m'});
      // Cookies.get("carts");
    },

    remove(cart) {
      const index = this.carts.indexOf(cart)
      this.carts.splice(index, 1)
      this.saveCats();
    },

    pop() {
      this.carts.pop()
    },
  }
}
</script>  