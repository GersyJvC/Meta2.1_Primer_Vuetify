<template>
  <v-card>
    <v-img :src="imagenSrc" height="300px"></v-img>
    <v-card-title>{{ titulo }}</v-card-title>
  </v-card>
</template>

<script>
export default {
  props: {
    imagenSrc: String,
    titulo: String
  }
};
</script>
