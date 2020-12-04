<template>
  <div>
    <b-navbar toggleable="lg" type="light">
      <div class="container">
        <b-navbar-brand href="#">Kuliner Nusantara</b-navbar-brand>

        <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

        <b-collapse id="nav-collapse" is-nav>
          <b-navbar-nav>
            <li class="nav-item">
              <router-link class="nav-link" to="/">Beranda</router-link>
            </li>
            <li class="nav-item">
              <router-link class="nav-link" to="/foods">Makanan</router-link>
            </li>
              <li class="nav-item">
              <router-link class="nav-link" to="/drinks">Minuman</router-link>
            </li>
             <li class="nav-item">
              <router-link class="nav-link" to="/tentang">Tentang</router-link>
            </li>
            
          </b-navbar-nav>

          <!-- Right aligned nav items -->
          <b-navbar-nav class="ml-auto">
            <ul class="navbar-nav ml-auto">
              <li class="nav-item">
                <router-link class="nav-link" to="/keranjang">
                  Keranjang
                  <b-icon-bag></b-icon-bag>
                  <span
                    class="badge badge-success ml-2"
                  >{{ updateKeranjang ? updateKeranjang.length : jumlah_pesanans.length}}</span>
                </router-link>
              </li>
            </ul>
          </b-navbar-nav>
        </b-collapse>
      </div>
    </b-navbar>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "Navbar",
  data() {
    return {
      jumlah_pesanans: []
    };
  },
  props: ["updateKeranjang"], // props adalah data yang di oper dari satu komponen ke komponen lain
  methods: {
    setJumlah(data) {
      this.jumlah_pesanans = data;
    }
  },
  mounted() {
    axios
      .get(
        "http://localhost:3000/keranjangs"
      ) /*URL ini diambil dari json placeholder tepatnya di tabel products */
      .then(response => this.setJumlah(response.data)) // jangan pake function karena akan error,karena function tidak di defenisikan.Lebih baik dihapus dan pake tanda panah
      .catch(error => console.log(error));
  }
};
</script>

<style>
</style>