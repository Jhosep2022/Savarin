<template>
  <v-row class="mt-10 mb-5">
    <v-col
      cols="12"
      xs="12"
      sm="6"
      md="4"
      v-for="(client, i) in clients"
      :key="i"
    >
      <v-card class="elevation-16 mx-auto" width="300">
        <v-list subheader two-line>
          <v-list-item>
            <v-list-item-avatar>
              <v-img :src="client.img"></v-img>
            </v-list-item-avatar>

            <v-list-item-content>
              <v-list-item-title>{{ client.title }}</v-list-item-title>
              <v-list-item-subtitle>{{ client.subtitle }}</v-list-item-subtitle>
            </v-list-item-content>
          </v-list-item>
        </v-list>
        <v-card-text>
          <div class="mt-n7">
            <v-rating
              v-model="rating"
              color="yellow darken-3"
              background-color="grey darken-1"
              empty-icon="$ratingFull"
              half-increments
              hover
              small
            ></v-rating>
          </div>
          <div v-html="client.bio"></div> <!-- Modificación aquí -->
        </v-card-text>
      </v-card>
    </v-col>
  </v-row>
</template>


<script>
export default {
  data: () => ({
    rating: 4.5,
  
    clients: [
      {
        img: "https://cdn.vuetifyjs.com/images/lists/1.jpg",
        title: "Kareem Benji",
        subtitle: "Que son?",
        bio: "Los diagramas de flujo son herramientas visuales ampliamente utilizadas en diversos campos para representar de manera gráfica los pasos de un proceso, sistema o algoritmo. Estas representaciones gráficas son especialmente útiles para entender la secuencia de acciones y decisiones en un sistema, así como para comunicar de manera clara y concisa cómo funciona un proceso.",
      },
      {
        img: "https://cdn.vuetifyjs.com/images/lists/2.jpg",
        title: "AAE IdeaPro",
        subtitle: "Tipos de diagramas de flujo",
        bio: "Los diagramas de flujo están compuestos por una serie de elementos:<br>Inicio/Fin: Representa el punto de inicio o finalización del proceso.<br>Proceso: Indica una acción o tarea específica que se lleva a cabo dentro del proceso.<br>Decisión: Representa un punto en el proceso donde se toma una decisión basada en una condición específica.<br>Conector: Se utiliza para conectar diferentes partes del diagrama y evitar la duplicación de líneas.<br>Entrada/Salida: Indica la entrada de datos al proceso o la salida de resultados."

      },
      {
      img: "https://cdn.vuetifyjs.com/images/lists/3.jpg",
      title: "Raul Seem",
      subtitle: "Beneficios",
      bio: "Claridad y comprensión: Permiten visualizar de manera clara y concisa la estructura y el flujo de un proceso.<br>Comunicación efectiva: Facilitan la comunicación entre diferentes personas o equipos al proporcionar una representación visual del proceso.<br>Identificación de problemas: Ayudan a identificar cuellos de botella, redundancias o ineficiencias en un proceso.<br>Documentación: Sirven como documentación visual que puede ser utilizada para propósitos de referencia o entrenamiento."
    },
    ],
  }),
};
</script>

<style>
</style>