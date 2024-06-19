<template>
    <v-card>
      <v-card-title>
        <span class="headline">Diagrama de Flujo</span>
        <v-card-actions>
          <v-btn color="success" @click="$emit('close', true)">Cerrar</v-btn>
        </v-card-actions>
      </v-card-title>
      <v-card-text>
        <iframe src="../../public/bernardodiramgra.jpg" width="100%" height="500px" style="border: none;" @load="onLoad" @error="onError"></iframe>
      </v-card-text>
    </v-card>
  </template>
  
  <script>
  export default {
    name: 'DiagramaDeFlujoModal',
    methods: {
      onLoad() {
        console.log('El iframe se ha cargado correctamente.');
      },
      onError(event) {
        console.error('Error al cargar el iframe:', event);
      }
    }
  };
  </script>
  
  <style scoped>
  .v-btn--primary {
    background-color: #28a745 !important; /* Verde */
  }
  </style>
  