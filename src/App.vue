<template>
  <v-app>
    <AppHeader />

    <v-container>
      <v-row justify="center">
        <v-col cols="12" sm="6">
          <TarjetaConImagen :imagenSrc="imagen1" titulo="Imagen 1" />
        </v-col>
        <v-col cols="12" sm="6">
          <TarjetaConImagen :imagenSrc="imagen2" titulo="Imagen 2" />
        </v-col>
      </v-row>

      <v-row justify="center">
        <v-col cols="12" class="text-center">
          <v-btn color="success" @click="refreshImages">Actualizar</v-btn>
          <v-progress-circular v-if="loading" indeterminate color="primary" class="ml-2"></v-progress-circular>
        </v-col>
      </v-row>

      <TablaDeDatos />
    </v-container>

    <AppFooter />
  </v-app>
</template>

<script>
import AppHeader from "./components/AppHeader.vue";
import TarjetaConImagen from "./components/TarjetaConImagen.vue";
import TablaDeDatos from "./components/TablaDeDatos.vue";
import AppFooter from "./components/AppFooter.vue";

export default {
  components: {
    AppHeader,
    TarjetaConImagen,
    TablaDeDatos,
    AppFooter
  },
  data() {
    return {
      imagen1: "https://picsum.photos/500/300",
      imagen2: "https://picsum.photos/501/300",
      loading: false
    };
  },
  methods: {
    async refreshImages() {
      this.loading = true;
      try {
        const res1 = await fetch("https://picsum.photos/500/300");
        const res2 = await fetch("https://picsum.photos/501/300");

        this.imagen1 = res1.url;
        this.imagen2 = res2.url;
      } catch (error) {
        console.error("Error al cargar imágenes:", error);
      } finally {
        this.loading = false;
      }
    }
  },
  mounted() {
    this.refreshImages();
  }
};
</script>
