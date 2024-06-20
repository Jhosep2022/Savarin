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
          <label for="numSimulaciones">Número de Simulaciones:</label>
          <input type="number" id="numSimulaciones" v-model="numSimulaciones" min="1" placeholder="Número de simulaciones">
        </div>
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
          <input type="text" id="pgve" v-model="pgve" placeholder="Ejemplo: 10%" @blur="formatPercentage">
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
                <th>Número de simulación</th>
                <th>Ganancia Neta</th>
                <th>Ganancia Neta Promedio por Semana</th>
                <th>Costo de Compra por Semana</th>
                <th>Demanda Insatisfecha Media General</th>
                <th>Demanda Insatisfecha de Cada Cerveza</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="(resultado, index) in resultados" :key="index">
                <td>{{ index + 1 }}</td>
                <td>{{ resultado.gananciaNeta }}</td>
                <td>{{ resultado.gananciaNetaSemanas }}</td>
                <td>{{ resultado.costoCompraSemana }}</td>
                <td>{{ resultado.demandaInsatisfechaMedia }}</td>
                <td>{{ JSON.stringify(resultado.demandaCervezas) }}</td>
              </tr>
            </tbody>
          </table>
        </div>
        <button class="descargar-button" @click="descargarExcel">Descargar Resultados en Excel</button>
      </div>
    </div>
    <div class="additional-results">
      <ResultadosSimulacion
        :visible="mostrarTabla"
        :gananciaNeta="calcularGananciaNeta()"
        :gananciaNetaSemanas="calcularGananciaNetaSemanas()"
        :costoCompraSemana="calcularCostoCompraSemana()"
        :demandaInsatisfechaMedia="calcularDemandaInsatisfechaMedia()"
        :demandaCervezas="calcularDemandaCervezas()"
      />
    </div>
  </div>
</template>

<script>
import VariablesDeEntorno from '../components/VariablesDeEntorno';
import DiagramaDeFlujoModal from '../components/DiagramaDeFlujoModal';
import { utils, writeFile } from 'xlsx';
import Navbar from "../components/Navbar";
import ResultadosSimulacion from "../components/ResultadosSimulacion";

export default {
  components: {
    VariablesDeEntorno,
    DiagramaDeFlujoModal,
    Navbar,
    ResultadosSimulacion
  },
  data() {
    return {
      numSimulaciones: '',
      ms: '',
      invMaxHuari: 300, 
      invMaxPacena: 210, 
      invMaxAmstel: 120, 
      maxClie: 150, 
      maxDA: 2,
      pgve: '',
      resultados: [],
      mostrarTabla: false,
      mensajeLimpieza: false,
      showDiagrama: false,
      precioVentaHuari: 23,
      precioVentaPacena: 20,
      precioVentaAmstel: 24,
      precioCompraHuari: 14.5,
      precioCompraPacena: 12,
      precioCompraAmstel: 13
    };
  },
  methods: {
    mostrarDiagrama() {
      this.showDiagrama = true;
    },
    simular() {
      if (isNaN(this.numSimulaciones) || this.numSimulaciones === '') {
        alert("Por favor, ingrese un número válido de simulaciones.");
        return;
      }
      if (isNaN(this.ms) || this.ms === '') {
        alert("Por favor, ingrese el número de semanas a simular.");
        return;
      }
      this.resultados = [];

      // Realizar las simulaciones
      for (let sim = 1; sim <= parseInt(this.numSimulaciones); sim++) {
        let acumGananciaNeta = 0;
        let acumCostoCompra = 0;
        let demandaTotal = {
          huari: 0,
          pacena: 0,
          amstel: 0
        };

        // Simular cada semana
        for (let semana = 1; semana <= parseInt(this.ms); semana++) {
          const ventasHuari = Math.min(this.generarDemanda(), this.invMaxHuari);
          const ventasPacena = Math.min(this.generarDemanda(), this.invMaxPacena);
          const ventasAmstel = Math.min(this.generarDemanda(), this.invMaxAmstel);

          const ingresosHuari = ventasHuari * this.precioVentaHuari;
          const ingresosPacena = ventasPacena * this.precioVentaPacena;
          const ingresosAmstel = ventasAmstel * this.precioVentaAmstel;

          const costoHuari = ventasHuari * this.precioCompraHuari;
          const costoPacena = ventasPacena * this.precioCompraPacena;
          const costoAmstel = ventasAmstel * this.precioCompraAmstel;

          // Acumular resultados
          acumGananciaNeta += (ingresosHuari + ingresosPacena + ingresosAmstel - costoHuari - costoPacena - costoAmstel);
          acumCostoCompra += (costoHuari + costoPacena + costoAmstel);

          demandaTotal.huari += ventasHuari;
          demandaTotal.pacena += ventasPacena;
          demandaTotal.amstel += ventasAmstel;

          this.invMaxHuari -= ventasHuari;
          this.invMaxPacena -= ventasPacena;
          this.invMaxAmstel -= ventasAmstel;
        }

        // Añadir los resultados consolidados de la simulación
        this.resultados.push({
          simulacion: sim,
          gananciaNeta: acumGananciaNeta,
          costoCompra: acumCostoCompra,
          demandaCervezas: demandaTotal
        });
      }

      this.mostrarTabla = true;
    },

    limpiar() {
      this.numSimulaciones = '';
      this.ms = '';
      this.invMaxHuari = 300;
      this.invMaxPacena = 210;
      this.invMaxAmstel = 120;
      this.maxClie = 150;
      this.maxDA = 2;
      this.pgve = '';
      this.resultados = [];
      this.mostrarTabla = false;
      this.mensajeLimpieza = false;
    },
    generarDemanda() {
      return Math.floor(Math.random() * this.maxClie) + 1;
    },
    formatPercentage() {
      let value = this.pgve.replace(/[^0-9.]/g, '');
      value = parseFloat(value);
      if (!isNaN(value) && value <= 100) {
        this.pgve = (value / 100).toFixed(2);
      } else {
        this.pgve = '';
        alert('Please enter a valid percentage value between 0 and 100.');
      }
    },
    descargarExcel() {
      const ws = utils.json_to_sheet(this.resultados.map((resultado, index) => ({
        "Número de simulación": index + 1,
        "Ganancia Neta": resultado.gananciaNeta,
        "Ganancia Neta Promedio por Semana": resultado.gananciaNetaSemanas,
        "Costo de Compra por Semana": resultado.costoCompraSemana,
        "Demanda Insatisfecha Media General": resultado.demandaInsatisfechaMedia,
        "Demanda Insatisfecha de Cada Cerveza": JSON.stringify(resultado.demandaCervezas)
      })));
      const wb = utils.book_new();
      utils.book_append_sheet(wb, ws, "Results");
      writeFile(wb, "simulation_results.xlsx");
    },
    calcularGananciaNeta() {
      return this.resultados.reduce((total, res) => total + (res.ingresosHuari + res.ingresosPacena + res.ingresosAmstel - res.costoHuari - res.costoPacena - res.costoAmstel), 0);
    },
    calcularGananciaNetaSemanas() {
      if (this.resultados.length === 0) return 0;
      let totalSemanas = this.resultados.reduce((total, res) => total + 1, 0);
      return this.calcularGananciaNeta() / totalSemanas;
    },
    calcularCostoCompraSemana() {
      if (this.resultados.length === 0) return 0;
      return this.resultados.reduce((total, res) => total + (res.costoHuari + res.costoPacena + res.costoAmstel), 0) / this.resultados.length;
    },
    calcularDemandaInsatisfechaMedia() {
      let totalDemandasInsatisfechas = this.resultados.reduce((total, res) => total + (this.maxClie - res.ventasHuari - res.ventasPacena - res.ventasAmstel), 0);
      return totalDemandasInsatisfechas / this.resultados.length;
    },
    calcularDemandaCervezas() {
      let demandaCervezas = {
        huari: this.resultados.reduce((total, res) => total + res.ventasHuari, 0),
        pacena: this.resultados.reduce((total, res) => total + res.ventasPacena, 0),
        amstel: this.resultados.reduce((total, res) => total + res.ventasAmstel, 0)
      };
      return demandaCervezas;
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
  width: 900px; 
  color: white;
  margin-bottom: 20px;
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
  width: 600px;
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 8px;
  background-color: #fff;
}

.result-table {
  min-width: 3000px; 
  width: 100%;
  border-collapse: collapse;
}

.result-table th, .result-table td {
  padding: 8px; 
  text-align: center;
  border: 1px solid #ccc;
}

.result-table th {
  background-color: #f2f2f2;
}

.table-wrapper {
  max-height: 450px;

  overflow-x: auto;
}

.additional-results {
  margin-top: 20px;

}
</style>
