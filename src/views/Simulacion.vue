<template>
  
  <div class="container">
    <Navbar /> 
    <header class="header">
      <img src="1.png" alt="Logo" class="logo">
      <h1>Depósito a Plazo Fijo</h1>
    </header>
    <div class="header-buttons">
      <VariablesDeEntorno />
      <div class="modal-buttons">
        <button @click="mostrarDiagrama" class="variables-de-entorno-button">Diagrama de Flujo</button>
        <v-dialog v-model="showDiagrama" max-width="800px" @close="showDiagrama = false">
          <DiagramaDeFlujoModal @close="showDiagrama = false" />
        </v-dialog>
      </div>
    </div>
    <p>¿Cuál será el capital en un depósito a plazo fijo bajo una tasa de interés constante?</p>
    <p class="instructions">Por favor, ingrese los siguientes datos para la Simulación:</p>
    <div class="simulation-parameters">
      <div class="form-section">
        <h2>Parámetros de la Simulación</h2>
        <div class="form-group">
          <label for="ms">Máximo de Semanas a Simular [MS]:</label>
          <input type="text" id="ms" v-model="ms" placeholder="MS" pattern="[0-9]*[.,]?[0-9]+" title="Ingrese un número válido">
        </div>
        <div class="form-group">
          <label for="invMaxHuari">Inventario Máximo Huari [InvMaxHuari]:</label>
          <input type="text" id="invMaxHuari" v-model="invMaxHuari" placeholder="InvMaxHuari" pattern="[0-9]*[.,]?[0-9]+" title="Ingrese un número válido">
        </div>
        <div class="form-group">
          <label for="invMaxPacena">Inventario Máximo Paceña [InvMaxPacena]:</label>
          <input type="text" id="invMaxPacena" v-model="invMaxPacena" placeholder="InvMaxPaceña" pattern="[0-9]*[.,]?[0-9]+" title="Ingrese un número válido">
        </div>
        <div class="form-group">
          <label for="invMaxAmstel">Inventario Máximo Amstel [InvMaxAmstel]:</label>
          <input type="text" id="invMaxAmstel" v-model="invMaxAmstel" placeholder="InvMaxAmstel" pattern="[0-9]*[.,]?[0-9]+" title="Ingrese un número válido">
        </div>
        <div class="form-group">
          <label for="maxClie">Capacidad Máxima de Clientes en el Restaurante [MaxClie]:</label>
          <input type="text" id="maxClie" v-model="maxClie" placeholder="MaxClie" pattern="[0-9]*[.,]?[0-9]+" title="Ingrese un número válido">
        </div>
        <div class="form-group">
          <label for="maxDA">Máximo Días de Atención en la Semana [MaxDA]:</label>
          <input type="text" id="maxDA" v-model="maxDA" placeholder="MaxDA" pattern="[0-9]*[.,]?[0-9]+" title="Ingrese un número válido">
        </div>
        <div class="form-group">
          <label for="pgve">Porcentaje Ganancia por Venta del Empleado [PGVE]:</label>
          <input type="text" id="pgve" v-model="pgve" placeholder="PGVE" pattern="[0-9]*[.,]?[0-9]+" title="Ingrese un número válido">
        </div>
        <div class="buttons">
          <button class="simular-button" @click="simular">Simular</button>
          <button class="limpiar-button" @click="limpiar">Limpiar</button>
        </div>
      </div>
      <div v-if="!mostrarTabla" class="result-section">
        <p>Por favor, ingrese los valores para la Simulación y presione 'Simular'.</p>
      </div>
      <div v-if="mostrarTabla" class="result-section">
        <p>Resultados de la simulación:</p>
        <div class="table-wrapper">
          <table v-if="resultados.length > 0" class="result-table">
            <thead>
              <tr>
                <th>Semana</th>
                <th>Cervezas Vendidas</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="(resultado, index) in resultados" :key="index">
                <td>{{ index + 1 }}</td>
                <td>{{ resultado }}</td>
                <td>{{ resultado }}</td>
                <td>{{ resultado }}</td>
                <td>{{ resultado }}</td>
              </tr>
            </tbody>
          </table>
        </div>
        <button class="descargar-button" @click="descargarExcel">Descargar Resultados en Excel</button>
      </div>
    </div>
  </div>
</template>

<script>
import VariablesDeEntorno from '../components/VariablesDeEntorno';
import DiagramaDeFlujoModal from '../components/DiagramaDeFlujoModal';
import { utils, writeFile } from 'xlsx';
import Navbar from "../components/Navbar";
export default {
  components: {
    VariablesDeEntorno,
    DiagramaDeFlujoModal,
    Navbar
  },
  data() {
    return {
      ms: '',
      invMaxHuari: '',
      invMaxPacena: '',
      invMaxAmstel: '',
      maxClie: '',
      maxDA: '2',
      pgve: '',
      resultados: [],
      mostrarTabla: false,
      mensajeLimpieza: false,
      showDiagrama: false
    };
  },
  methods: {
    mostrarDiagrama() {
      this.showDiagrama = true;
    },
    simular() {
      if (isNaN(this.ms) || isNaN(this.invMaxHuari) || isNaN(this.invMaxPacena) || isNaN(this.invMaxAmstel) || isNaN(this.maxClie) || isNaN(this.maxDA) || isNaN(this.pgve)) {
        alert("Por favor, ingrese solo números en los campos.");
        return;
      }

      const cervezasPorSemana = (parseFloat(this.invMaxHuari) + parseFloat(this.invMaxPacena) + parseFloat(this.invMaxAmstel)) * parseFloat(this.maxClie) * parseFloat(this.maxDA) * parseFloat(this.pgve) / 100;

      this.resultados = [];

      for (let semana = 1; semana <= parseFloat(this.ms); semana++) {
        this.resultados.push(cervezasPorSemana);
      }

      this.mostrarTabla = true;
      this.mensajeLimpieza = false;
    },
    limpiar() {
      this.ms = '';
      this.invMaxHuari = '';
      this.invMaxPacena = '';
      this.invMaxAmstel = '';
      this.maxClie = '';
      this.maxDA = '';
      this.pgve = '';

      this.resultados = [];

      this.mostrarTabla = false;
      this.mensajeLimpieza = true;
    },
    descargarExcel() {
      const ws = utils.json_to_sheet(this.resultados.map((resultado, index) => ({
        Semana: index + 1,
        "Cervezas Vendidas": resultado
      })));

      const wb = utils.book_new();
      utils.book_append_sheet(wb, ws, "Resultados");
      writeFile(wb, "resultados_simulacion.xlsx");
    }
  }
};
</script>

<style scoped>
.container {
  font-family: 'Montserrat', sans-serif;
  text-align: center;
  padding: 20px;
}

.header {
  display: flex;
  align-items: center;
  justify-content: center;
}

.logo {
  width: 50px;
  height: auto;
  margin-right: 20px;
}

.instructions {
  margin-top: 20px;
  font-size: 1.2em;
}

.simulation-parameters {
  display: flex;
  justify-content: center;
  margin-top: 20px;
}

.header-buttons {
  display: flex;
  justify-content: space-around; 
  align-items: center;
  margin-bottom: 20px;
}

.form-section {
  background-color: #7fbe8e;
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 8px;
  width: 600px;
  color: white;
}

.form-group {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-bottom: 20px;
}

.form-group label {
  font-weight: bold;
  margin-right: 10px;
  flex: 1;
}

.form-group input {
  flex: 1;
  padding: 10px;
  border-radius: 4px;
  border: 1px solid #ccc;
  background-color: #ffffff;
  color: rgb(0, 0, 0);
}

.buttons {
  display: flex;
  justify-content: space-between;
}

.simular-button {
  background-color: #007bff;
  color: white;
  padding: 10px 20px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.limpiar-button {
  background-color: #dc3545;
  color: white;
  padding: 10px 20px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.descargar-button {
  background-color: #007bff;
  color: white;
  padding: 10px 20px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  margin-top: 20px;
}

.modal-buttons {
  display: flex;
  justify-content: space-around; 
  margin-top: 0px;
}

.variables-de-entorno-button {
  background-color: #28a745;
  color: white;
  padding: 10px 20px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.result-section {
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 8px;
  margin-left: 20px;
}

.result-table {
  width: 100%;
  border-collapse: collapse;
  margin-top: 20px;
}

.result-table th,
.result-table td {
  border: 1px solid #ccc;
  padding: 8px;
  text-align: center;
}

.result-table th {
  background-color: #f2f2f2;
}

.table-wrapper {
  max-height: 429px;
  overflow-y: auto; 
}
</style>
