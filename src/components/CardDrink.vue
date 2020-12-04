<template>
<!--  <meta name="dicoding:email" content="rachelgultom5@gmail.com"> -->
  <!-- <h2>{{ product.nama }}</h2> -->
  <div class="card shadow card-drink">
    <img :src="'assets/images/' + drink.gambar" class="card-img-top" alt="..." /> 
    <div class="card-body">
      <h5 class="card-title">{{ drink.nama }}</h5>
      <p
        class="card-text"
      >Harga : Rp. {{drink.harga}}</p>
      <router-link :to ="'/drinks/' + drink.id" class="btn btn-success"><b-icon-cart></b-icon-cart> Pesan</router-link>
    </div>
  </div>
</template>

<script>
export default {
  name: "CardDrink",
  props: ["drink"]
};
</script>

<style>
</style>