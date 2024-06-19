<template>
  <v-app-bar app color="white" flat>
    <v-badge color="#D5F0DB" dot>
      <v-img src="loguito.jpg" contain width="40"></v-img>
    </v-badge>

    <v-toolbar-title class="ml-4">
      <strong>Savarin</strong>
    </v-toolbar-title>

    <v-spacer></v-spacer>
    
    <v-btn icon class="mx-15" @click="$router.push('/Simulacion')">
      Simulacion
    </v-btn>

    <span class="grey--text d-none d-sm-flex">
      Hola, <strong> Bernardo</strong>
    </span>
    
    <v-avatar size="30" class="ml-2">
      <v-img src="Berna.jpg"></v-img>
    </v-avatar>
  </v-app-bar>
</template>

<script>
export default {};
</script>

<style>
.v-toolbar__title {
  font-size: 1rem !important;
}
.mx-3 {
  margin-left: 1rem !important;
  margin-right: 1rem !important;
}
.bordered-icon {
  border: 2px solid #000; /* Puedes cambiar el color y grosor del borde */
  border-radius: 50%;
}
</style>
