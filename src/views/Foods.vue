<template>
  <div>
    <Navbar />
    <div class="container">
      <div class="row mt-4">
        <div class="col">
          <h2>
            Daftar
            <strong>Makanan</strong>
          </h2>
        </div>
      </div>

      <div class="row mt-3">
        <div class="col">
          <div class="input-group mb-3">
            <!-- v-model ini akan kita gunakan sebagai variabel dari search.Jadi supaya bisa melakukan pencarian otomatis,maka perlu ditambahkan kata kunci yaitu search -->
            <input
            v-model="search" 
              type="text"
              class="form-control"
              placeholder="Cari Makanan Kesukaan Anda.."
              aria-label="Cari"
              aria-describedby="basic-addon1"
              @keyup="searchFood"
            />
             <!-- fungsi keyup ini ketika kita ketik kata kunci,maka otomatis kata kunci itu akan mencari nilai dari fungsi si search food.Jadi search food akan melempar datanya ke sini lalau kita panggil-->
            <div class="input-group-prepend">
              <span class="input-group-text" id="basic-addon1">
                <b-icon-search></b-icon-search>
              </span>
            </div>
          </div>
        </div>
      </div>

      <div class="row mb-4">
        <div class="col-md-4 mt-4" v-for="product in products" :key="product.id">
          <!-- products ini dialiaskan untuk product -->
          <CardProduct :product="product" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import Navbar from "@/components/Navbar.vue";
import CardProduct from "@/components/CardProduct.vue";
import axios from "axios";

export default {
  name: "Foods",
  components: {
    Navbar,
    CardProduct
  },
  data() {
    return {
      /*disini akan dilempar value dari si db.json dengan tabel si best produts dari json placeholder */
      products: [],
      search: "" /* ini kita kosongkan pertama untuk menampung datanya */
    };
  },
  methods: {
    /*disini data akan diambil dari json placeholder lalu dimasukkan ke dalam products */
    setProducts(data) {
      this.products = data;
    },
    searchFood() { // disini kita akan buat pencarian dengan memanfaatkan axios dengan q sebagai parameter atau value yang akan di cari
      axios
        .get(
          "http://localhost:3000/products?q=" + this.search
        ) /*URL ini diambil dari json placeholder tepatnya di tabel products */
        .then(response => this.setProducts(response.data)) // jangan pake function karena akan error,karena function tidak di defenisikan.Lebih baik dihapus dan pake tanda panah
        .catch(error => console.log(error));
    }
  },
  /* ketika halaman home dipasang ,fungsi dalam mounted ini akan berjalan . Image result for fungsi mounted vue
Mounting merupakan tipe lifecycle pada Vue yang memungkinkan kita untuk mengakses dom persis sebelum dan sesudah template di-render. Jangan gunakan lifecycle tipe ini untuk keperluan mengambil data dan event, karena template membutuhkan data tersebut sebelum ditampilkan*/
  mounted() {
    // Make a request for a user with a given ID
    axios
      .get(
        "http://localhost:3000/products"
      ) /*URL ini diambil dari json placeholder tepatnya di tabel products */
      .then(response => this.setProducts(response.data)) // jangan pake function karena akan error,karena function tidak di defenisikan.Lebih baik dihapus dan pake tanda panah
      .catch(error => console.log(error));
  }
};
</script>


<style>
</style>