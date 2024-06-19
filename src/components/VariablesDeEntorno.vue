<template>
    <div class="variables-de-entorno">
      <button @click="mostrarVariables" class="variables-de-entorno-button">Variables de Entorno</button>
      <v-dialog v-model="showVariables" max-width="600px" @close="showVariables = false">
        <VariablesDeEntornoModal @close="showVariables = false" />
      </v-dialog>
    </div>
  </template>
  
  <script>
  import VariablesDeEntornoModal from './VariablesDeEntornoModal.vue';
  
  export default {
    components: {
      VariablesDeEntornoModal
    },
    data() {
      return {
        showVariables: false
      };
    },
    methods: {
      mostrarVariables() {
        this.showVariables = true;
      }
    }
  };
  </script>
  
  <style scoped>
  .variables-de-entorno-button {
    background-color: #28a745; /* Verde */
    color: white; /* Letras blancas */
    padding: 10px 20px;
    border: none;
    border-radius: 4px;
    cursor: pointer;
  }
  </style>
  