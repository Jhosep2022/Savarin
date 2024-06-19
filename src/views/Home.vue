<template>
  <v-app>
    <Navbar />
    <v-container fluid>
      <v-row>
        <v-col cols="12">
          <v-card class="mx-auto rounded-xl" flat>
            <v-img src="homesimu.jpg" height="400px" width="100%" contain>
              <v-card-title class="top ml-10">
                  <h2 class="title1">Bienvenidos</h2>
              </v-card-title>
              <v-card-title class="ml-10 mt-n8">
                  <h2 class="title2">Simulacion</h2>
              </v-card-title>
              <v-card-text class="ml-10">
                <h3 class="green--text">Modelado</h3>
              </v-card-text>
              <v-card-text class="ml-10">
                  
              </v-card-text>
          </v-img>
      </v-card>


          <v-card flat color="#FAFAFA" class="mt-8 py-5 px-16">
            <div
              style="
                position: absolute;
                margin-left: auto;
                margin-right: auto;
                left: 0;
                right: 0;
                text-align: center;
              "
            >
              <h3>Diagramas de Flujo</h3>
            </div>
            <Client />
          </v-card>

          <v-toolbar flat color="transparent">
            <v-toolbar-title class="text-h6">Category</v-toolbar-title>
            <v-spacer></v-spacer>
            <v-btn-toggle v-model="toggle_exclusive" group color="#49D9A0">
              <v-btn>
                <v-icon>mdi-chevron-left</v-icon>
              </v-btn>
              <v-btn>
                <v-icon>mdi-chevron-right</v-icon>
              </v-btn>
            </v-btn-toggle>
          </v-toolbar>

          <Category />

          <v-toolbar flat color="transparent" class="mt-5">
            <v-toolbar-title class="text-h6">Simulacion</v-toolbar-title>
            <v-spacer></v-spacer>
            <v-btn rounded color="green" dark class="px-8">See All</v-btn>
          </v-toolbar>
          <Product />
          
          <v-toolbar flat color="transparent" class="mt-8">
            <v-toolbar-title class="text-h6"
              >Our Trusted Partner</v-toolbar-title
            >
          </v-toolbar>
          
          <v-card
            flat
            color="#E2F2E5"
            class="rounded-xl mtop mbottom mx-10 pa-4"
            height="350"
          >
            <v-row>
              <v-col cols="12" xs="12" sm="12" md="5">
                <v-card
                  class="rounded-xl mt-n16 ml-16 mobile"
                  outlined
                  flat
                  height="450"
                  width="200"
                >
                <v-img src="diagramaflujo.jpg" height="100%" width="100%"></v-img>
                </v-card>
              </v-col>
              <v-col cols="12" xs="12" sm="6" md="7">
                <h1 class="mt-16">Caracteristicas del Restaurante</h1>
                <p>
                  El Savarin es un restaurante popular en La Paz, Bolivia, conocido por su
                  variada oferta de platos tradicionales y bebidas. Ubicado estratégicamente
                  cerca de la terminal de buses, el restaurante opera únicamente los fines de
                  semana, atrayendo a una clientela diversa. La optimización de su gestión es
                  esencial para maximizar la eficiencia operativa y mejorar la experiencia del
                  cliente.
                </p>
              </v-col>
            </v-row>
          </v-card>
        </v-col>
      </v-row>
    </v-container>
    <Footer />
  </v-app>
</template>

<script>
import Navbar from "../components/Navbar";
import Footer from "../components/Footer";
import Category from "../components/Category.vue";
import Product from "../components/Product.vue";
import Client from "../components/Client.vue";

export default {
  name: "Home",
  data: () => ({
    toggle_exclusive: 1,
  }),
  components: {
    Navbar,
    Footer,
    Category,
    Product,
    Client,
    
  },
};
</script>
<style >
.marginLeft {
  margin-left: -90px;
}
.mtop {
  margin-top: 100px;
}
.mbottom {
  margin-bottom: 100px;
}
.v-card.borderme {
  border: 2px solid green !important;
}
.v-card.borderout {
  border: 1px solid #d5f0db !important;
}
.v-btn:not(.v-btn--round).v-size--default.add {
  min-width: 0px !important;
}
.theme--light.v-sheet--outlined.mobile {
  border: 2px solid black !important;
}
@media only screen and (max-width: 600px) {
  h2.title1 {
    font-size: 15px;
  }
  h2.title2 {
    font-size: 15px;
  }
  .top {
    margin-top: 20px;
  }
}
@media only screen and (min-width: 600px) {
  .top {
    margin-top: 70px;
  }
}
@media only screen and (min-width: 768px) {
  .top {
    margin-top: 120px;
  }
}
</style>
