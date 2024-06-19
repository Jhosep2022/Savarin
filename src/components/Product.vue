<template>
  <v-row justify="center" class="space px-16">
    <v-col
      cols="12"
      xs="12"
      sm="6"
      md="4"
      v-for="(product, i) in products"
      :key="i"
    >
      <v-card class="mx-auto rounded-xl" max-width="300" color="" flat outlined>
        <div align="center" justify="center">
          <v-img
            max-height="300"
            max-width="300"
            contain
            :src="product.img"
          ></v-img>
        </div>

        <v-card-title class="">{{ product.title }}</v-card-title>
        <v-card-title class="grey--text text-grey-darken-1 caption mt-n6">{{
          product.subtitle
        }}</v-card-title>
        <v-card-title class="mt-n4">{{ product.price }}</v-card-title>

      
      </v-card>
    </v-col>
  </v-row>
</template>

<script>
export default {
  data: () => ({
      bpm: 1,
    products: [
      { img: "paceñita.png", title: "Paceña", subtitle: "150ml", price: "$13" },
      { img: "amstel.png", title: "Amstel", subtitle: "150ml", price: "$23" },
      { img: "huarili.png", title: "Huari", subtitle: "150ml", price: "$17" },
    ],
  }),
   methods: {
      decrement () {
        this.bpm--
      },
      increment () {
        this.bpm++
      },
     
    },
};
</script>

<style>
</style>