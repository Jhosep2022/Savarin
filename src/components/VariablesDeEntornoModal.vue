<template>
    <v-card>
      <v-card-title>
        <span class="headline">Variables de Entorno</span>
        <v-card-actions>
        <v-btn color="success" @click="$emit('close', true)">Cerrar</v-btn>
      </v-card-actions>
      </v-card-title>
      <v-card-text>
        <v-simple-table>
          <template v-slot:default>
            <thead>
              <tr>
                <th class="text-left">Nro.</th>
                <th class="text-left">Nombre Variable</th>
                <th class="text-left">Sigla</th>
                <th class="text-left">Clasificación</th>
                <th class="text-left">Unidades</th>
                <th class="text-left">Descripción</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="(variable, index) in variables" :key="index">
                <td>{{ index + 1 }}</td>
                <td>{{ variable.nombre }}</td>
                <td>{{ variable.sigla }}</td>
                <td>{{ variable.clasificacion }}</td>
                <td>{{ variable.unidades }}</td>
                <td>{{ variable.descripcion }}</td>
              </tr>
            </tbody>
          </template>
        </v-simple-table>
      </v-card-text>
      
    </v-card>
  </template>
  
  <script>
  export default {
    data() {
  return {
    variables: [
      { nombre: 'Contador semanas', sigla: 'CS', clasificacion: 'Endogena', unidades: 'Semanas', descripcion: '' },
      { nombre: 'Contador días', sigla: 'CD', clasificacion: 'Endogena', unidades: 'Días', descripcion: '' },
      { nombre: 'Contador de cerveza huari', sigla: 'Chuari', clasificacion: 'Endogena', unidades: 'Cerveza', descripcion: '' },
      { nombre: 'Contador total huari', sigla: 'CThuari', clasificacion: 'Endogena', unidades: 'Cerveza', descripcion: '' },
      { nombre: 'Cant repocicion huari', sigla: 'Rephuari', clasificacion: 'Endogena', unidades: 'Cerveza', descripcion: '' },
      { nombre: 'Faltante huari', sigla: 'Falhuari', clasificacion: 'Endogena', unidades: 'Cerveza', descripcion: '' },
      { nombre: 'Inventario maximo huari', sigla: 'InvMaxHuari', clasificacion: 'Exogena', unidades: 'Cajas de cerveza', descripcion: '' },
      { nombre: 'Inventario huari', sigla: 'InvHuari', clasificacion: 'Endogena', unidades: 'Cajas de cerveza', descripcion: '' },
      { nombre: 'Cantidad total repocicion huari', sigla: 'CTRephuari', clasificacion: 'Endogena', unidades: '', descripcion: '' },
      { nombre: 'Precio compra huari', sigla: 'PChuari', clasificacion: 'Exogena', unidades: '', descripcion: '' },
      { nombre: 'Contador de cerveza paceña', sigla: 'Cpaceña', clasificacion: 'Endogena', unidades: '', descripcion: '' },
      { nombre: 'Contador total paceña', sigla: 'CTpaceña', clasificacion: 'Endogena', unidades: '', descripcion: '' },
      { nombre: 'Cantidad reposicion paceña', sigla: 'Reppaceña', clasificacion: 'Endogena', unidades: '', descripcion: '' },
      { nombre: 'Faltante paceña', sigla: 'Falpaceña', clasificacion: 'Endogena', unidades: '', descripcion: '' },
      { nombre: 'Inventario maximo paceña', sigla: 'InvMaxPaceña', clasificacion: 'Exogena', unidades: '', descripcion: '' },
      { nombre: 'Inventario paceña', sigla: 'InvPaceña', clasificacion: 'Endogena', unidades: '', descripcion: '' },
      { nombre: 'Cantitad total de reposicion paceña', sigla: 'CTReppaceña', clasificacion: 'Endogena', unidades: '', descripcion: '' },
      { nombre: 'Precio compra paceña', sigla: 'PCpaceña', clasificacion: 'Exogena', unidades: '', descripcion: '' },
      { nombre: 'Contador de cerveza amstel', sigla: 'Camstel', clasificacion: 'Endogena', unidades: '', descripcion: '' },
      { nombre: 'Contador total amstel', sigla: 'CTamstel', clasificacion: 'Endogena', unidades: '', descripcion: '' },
      { nombre: 'Reposicion amstel', sigla: 'Repamstel', clasificacion: 'Endogena', unidades: '', descripcion: '' },
      { nombre: 'Faltante amstel', sigla: 'Falamstel', clasificacion: 'Endogena', unidades: '', descripcion: '' },
      { nombre: 'Inventario maximo amstel', sigla: 'InvMaxAmstel', clasificacion: 'Exogena', unidades: '', descripcion: '' },
      { nombre: 'Inventario amstel', sigla: 'InvAmstel', clasificacion: 'Endogena', unidades: '', descripcion: '' },
      { nombre: 'Cantitad total reposicion amstel', sigla: 'CTRepamstel', clasificacion: 'Endogena', unidades: '', descripcion: '' },
      { nombre: 'Precio compra amstel', sigla: 'PCamstel', clasificacion: 'Exogena', unidades: '', descripcion: '' },
      { nombre: 'Sumatoria total de compras', sigla: 'CompraS', clasificacion: 'Endogena', unidades: '', descripcion: '' },
      { nombre: 'Contador total reposicion', sigla: 'CTRep', clasificacion: 'Endogena', unidades: '', descripcion: '' },
      { nombre: 'Salario mesero', sigla: 'SM', clasificacion: 'Endogena', unidades: '', descripcion: '' },
      { nombre: 'Costo total', sigla: 'CT', clasificacion: 'Endogena', unidades: '', descripcion: '' },
      { nombre: 'Maximo de semanas', sigla: 'MS', clasificacion: 'Endogena', unidades: '', descripcion: '' },
      { nombre: 'Precio de venta huari', sigla: 'PVHuari', clasificacion: 'Exogena', unidades: '', descripcion: '' },
      { nombre: 'Precio de venta paceña', sigla: 'PVPaceña', clasificacion: 'Exogena', unidades: '', descripcion: '' },
      { nombre: 'Precio de venta amstel', sigla: 'PVAmstel', clasificacion: 'Exogena', unidades: '', descripcion: '' },
      { nombre: 'Ganancia neta', sigla: 'GN', clasificacion: 'Endogena', unidades: '', descripcion: '' },
      { nombre: 'Ganancia bruta', sigla: 'GB', clasificacion: 'Endogena', unidades: '', descripcion: '' },
      { nombre: 'Costo por semana huari', sigla: 'CPShuari', clasificacion: 'Endogena', unidades: '', descripcion: '' },
      { nombre: 'Costo por semana paceña', sigla: 'CPSpaceña', clasificacion: 'Endogena', unidades: '', descripcion: '' },
      { nombre: 'Costo por semana amstel', sigla: 'CPSamstel', clasificacion: 'Endogena', unidades: '', descripcion: '' },
      { nombre: 'Media demanda insatisfecha', sigla: 'MDI', clasificacion: 'Endogena', unidades: '', descripcion: '' },
      { nombre: 'Demanda insatisfecha de huari', sigla: 'DIhuari', clasificacion: 'Endogena', unidades: '', descripcion: '' },
      { nombre: 'Demanda insatisfecha de paceña', sigla: 'DIpaceña', clasificacion: 'Endogena', unidades: '', descripcion: '' },
      { nombre: 'Demanda insatisfecha de amstel', sigla: 'DIamstel', clasificacion: 'Endogena', unidades: '', descripcion: '' },
      { nombre: 'Numero aleatorio de clientes', sigla: 'Aclie', clasificacion: 'Estado', unidades: '', descripcion: '' },
      { nombre: 'Maximo clientes por día', sigla: 'MClie', clasificacion: 'Exogena', unidades: '', descripcion: '' },
      { nombre: 'Contador clientes', sigla: 'ContCLI', clasificacion: 'Endogena', unidades: '', descripcion: '' },
      { nombre: 'Aleatorio de cerveza', sigla: 'Acerv', clasificacion: 'Estado', unidades: '', descripcion: '' },
      { nombre: 'Aleatorio de cantidad de cerveza', sigla: 'Acant', clasificacion: 'Estado', unidades: '', descripcion: '' },
      { nombre: 'Cantidad', sigla: 'Cant', clasificacion: 'Endogena', unidades: '', descripcion: '' },
      { nombre: 'Maximo de clientes dentro del restaurante', sigla: 'MaxClie', clasificacion: 'Exogena', unidades: '', descripcion: '' },
        { nombre: 'Maximo Dias de Atencion en la semana', sigla: 'MaxDA', clasificacion: 'Exogena', unidades: '', descripcion: '' },
        { nombre: 'Porcentaje Ganacia x Venta del Empleado', sigla: 'PGVE', clasificacion: 'Endogena', unidades: '', descripcion: '' },
        ]
      };
    }
  };
  </script>
  <style scoped>
  .v-btn--primary {
    background-color: #28a745 !important; /* Verde */
  }
  </style>