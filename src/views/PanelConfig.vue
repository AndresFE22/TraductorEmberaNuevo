<template>
    <v-app>
      <v-container>
        <v-row>
          <!-- Formulario para agregar palabras -->
          <v-col cols="12" sm="6" md="4">
            <v-card>
              <v-card-title class="teal">
                <h2 class="white--text">Introducir palabras</h2>
              </v-card-title>
              <v-card-text>
                <v-form @submit.prevent="agregarPalabra">
                  <v-text-field v-model="espanol" label="Agregue palabra en español" required></v-text-field>
                  <v-text-field v-model="embera" label="Agregue palabra en embera" required></v-text-field>
                  <v-btn type="submit" color="teal">Guardar</v-btn>
                </v-form>
              </v-card-text>
            </v-card>
          </v-col>
  
          <!-- Tabla para mostrar palabras -->
          <v-col cols="12" sm="6" md="8">
            <v-card>
              <v-card-title class="teal">
                <h2 class="white--text">Palabras Registradas</h2>
              </v-card-title>
              <v-card-text>
                <v-data-table :headers="headers" :items="palabras" item-key="id" class="elevation-1">
                <template v-slot:items="props">
                  <tr v-for="(palabra, index) in props.item" :key="index">
                    <td>{{ palabra }}</td>
                  </tr>
                </template>
              </v-data-table>
              </v-card-text>
            </v-card>
          </v-col>
        </v-row>
      </v-container>
    </v-app>
  </template>
  
  <script>
import axios from 'axios'

export default {
    data() {
      return {
        espanol: "",
        embera: "",
        palabras: [], 
        headers: [
          { text: "Español", value: 'espanol'},
          { text: "Embera", value: 'embera' },
        ],
      };
    },
    methods: {
      agregarPalabra() {
        const paquete = 
        {
      espanol: this.espanol,
      embera: this.embera
    }
        axios.post(`http://127.0.0.1:5000/palabras`, { paquete: paquete }) 
        .then(response => {
          this.message = response.data.message
          this.obtenerPalabras()
          this.espanol = ""
          this.embera = ""
        })
        .catch(error => {
          console.error(error);
        });
      },
      obtenerPalabras() {
        axios.get(`http://127.0.0.1:5000/obtener`) 
        .then(response => {
          this.palabras = response.data || [];
          console.log(this.palabras)
        })
        .catch(error => {
          console.error(error);
        });
      },
    },
    created() {
      this.obtenerPalabras();
    },
  };
  </script>
  
  <style scoped>
  /* Estilos específicos del componente si es necesario */
  </style>
  