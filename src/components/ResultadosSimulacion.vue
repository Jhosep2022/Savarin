<template>
    <div v-if="visible" class="resultados-simulacion">
      <h3>Resultados Adicionales de la Simulación</h3>
      <ul>
        <li>Ganancia Neta: {{ gananciaNeta }}</li>
        <li>Ganancia Neta Promedio por Semana: {{ gananciaNetaSemanas }}</li>
        <li>Costo de Compra por Semana de Cada Cerveza: {{ costoCompraSemana }}</li>
        <li>Demanda Insatisfecha Media General: {{ demandaInsatisfechaMedia }}</li>
        <li>Demanda Insatisfecha de Cada Cerveza: {{ demandaCervezas }}</li>
      </ul>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      visible: Boolean,
      gananciaNeta: Number,
      gananciaNetaSemanas: Number,
      costoCompraSemana: Number,
      demandaInsatisfechaMedia: Number,
      demandaCervezas: Object
    }
  }
  </script>
  
  <style scoped>
  .resultados-simulacion {
    margin-top: 20px;
    padding: 15px;
    background-color: #f9f9f9;
    border-radius: 8px;
    border: 1px solid #ccc;
  }
  
  .resultados-simulacion h3 {
    color: #333;
  }
  
  .resultados-simulacion ul {
    list-style-type: none;
    padding: 0;
  }
  </style>
  