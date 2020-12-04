
<template>
  <div class="home">
    <Navbar />
    <div class="container">
      <Hero />
      <div class="row mt-4">
        <div class="col">
          <h2>
            Best
            <strong>Foods</strong>
          </h2>
        </div>
        <div class="col">
          <router-link to="/foods" class="btn btn-success float-right">
            <b-icon-eye></b-icon-eye> Lihat Semua
          </router-link>
        </div>
      </div>

    

      <div class="row mb-4">
        <div class="col-md-4 mt-4" v-for="product in products"  :key="product.id"> <!-- products ini dialiaskan untuk product -->
          <CardProduct :product="product"/>
        </div>
      </div>

        <!-- drinks 
        <div class="row mt-4">
        <div class="col">
          <h2>
            Best
            <strong>Drinks</strong>
          </h2>
        </div>
        <div class="col">
          <router-link to="/drinks" class="btn btn-success float-right">
            <b-icon-eye></b-icon-eye> Lihat Semua
          </router-link>
        </div>
      </div> -->

       <div class="row mb-4">
        <div class="col-md-4 mt-4" v-for="drink in drinks"  :key="drink.id"> <!-- products ini dialiaskan untuk product -->
          <CardDrink :drink="drink"/>
        </div>
      </div>

    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import Navbar from "@/components/Navbar.vue";
import Hero from "@/components/Hero.vue";
import CardProduct from "@/components/CardProduct.vue";
import CardDrink from "@/components/CardDrink.vue";
import axios from "axios";

export default {
  name: "Home",
  components: {
    Navbar,
    Hero,
    CardProduct,
    CardDrink,
  },

  data() {
    return {
      /*disini akan dilempar value dari si db.json dengan tabel si best produts dari json placeholder */
      products: [],
      drinks: [],
    };
  },
  methods: {
    /*disini data akan diambil dari json placeholder lalu dimasukkan ke dalam products */
    setProducts(data) {
      this.products = data;
    },
    setDrinks(data){
      this.drinks = data;
    }
  },
  /* ketika halaman home dipasang ,fungsi dalam mounted ini akan berjalan . Image result for fungsi mounted vue
Mounting merupakan tipe lifecycle pada Vue yang memungkinkan kita untuk mengakses dom persis sebelum dan sesudah template di-render. Jangan gunakan lifecycle tipe ini untuk keperluan mengambil data dan event, karena template membutuhkan data tersebut sebelum ditampilkan*/
  mounted() {
    // Make a request for a user with a given ID
    axios
      .get("http://localhost:3000/best-products") /*URL ini diambil dari json placeholder tepatnya di tabel products */
      .then((response) => this.setProducts(response.data))// jangan pake function karena akan error,karena function tidak di defenisikan.Lebih baik dihapus dan pake tanda panah
      .catch((error) =>  console.log(error))

      axios
      .get("http://localhost:3000/best-drinks") /*URL ini diambil dari json placeholder tepatnya di tabel products */
      .then((response) => this.setDrinks(response.data))// jangan pake function karena akan error,karena function tidak di defenisikan.Lebih baik dihapus dan pake tanda panah
      .catch((error) =>  console.log(error))
  },
};
</script>
