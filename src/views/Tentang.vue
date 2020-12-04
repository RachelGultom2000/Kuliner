<template>
  <div class="tentang">
    <Navbar />
    <div class="container">
      <div class="row justify-content-center mt-5">
        <div class="col text-center">
          <h4><Strong>Kuliner Nusantara</Strong> adalah website yang menawarkan makanan asli Indonesia yang di buat oleh para pelaku UMKM lokal.
            Dengan website ini,kiranya dapat membantu perekonomian UMKM lokal di Indonesia ditengah pandemi saat ini.
          </h4>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Navbar from "@/components/Navbar.vue";

export default {
  name: "Tentang",
  components: {
    Navbar
  }
};
</script>

<style>
</style>