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
                  <v-text-field v-model="wayuu" label="Agregue palabra en wayuunaiky" required></v-text-field>
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
                    <td>{{ props.item.espanol }}</td>
                    <td>{{ props.item.wayuu }}</td>
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
  export default {
    data() {
      return {
        espanol: "",
        wayuu: "",
        palabras: [], // Aquí se almacenarán las palabras obtenidas del backend
        headers: [
          { text: "Español", value: "espanol" },
          { text: "Wayuu", value: "wayuu" },
        ],
      };
    },
    methods: {
      async agregarPalabra() {
        // Lógica para agregar la palabra al backend
        // Aquí puedes realizar una llamada a la API para agregar la palabra
  
        // Ejemplo: Supongamos que tienes una función en tu servicio que agrega la palabra
        try {
          await this.$servicioPalabras.agregarPalabra({
            espanol: this.espanol,
            wayuu: this.wayuu,
          });
  
          // Actualizar la lista de palabras después de agregar una nueva
          this.obtenerPalabras();
          // Reiniciar los campos
          this.espanol = "";
          this.wayuu = "";
        } catch (error) {
          console.error("Error al agregar la palabra:", error);
        }
      },
      async obtenerPalabras() {
        // Lógica para obtener palabras del backend
        // Aquí puedes realizar una llamada a la API para obtener la lista de palabras
  
        // Ejemplo: Supongamos que tienes una función en tu servicio que obtiene las palabras
        try {
          this.palabras = await this.$servicioPalabras.obtenerPalabras();
        } catch (error) {
          console.error("Error al obtener las palabras:", error);
        }
      },
    },
    created() {
      // Al cargar el componente, obtener la lista de palabras
      this.obtenerPalabras();
    },
  };
  </script>
  
  <style scoped>
  /* Estilos específicos del componente si es necesario */
  </style>
  