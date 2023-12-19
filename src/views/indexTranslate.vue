<template>
    <v-app>
      <!-- App Bar -->
      <v-app-bar app>
        <v-app-bar-nav-icon @click.stop="drawer = !drawer"></v-app-bar-nav-icon>
        <v-img
          src="ruta_de_tu_imagen_icono.jpg"
          max-height="40"
          contain
          class="mr-4"
        ></v-img>
        <v-app-bar-title>Traductor Embera</v-app-bar-title>
        <v-spacer></v-spacer>
        <v-btn icon>
          <v-icon @click="openUserMenu">mdi-account</v-icon>
        </v-btn>
      </v-app-bar>
  
      <v-navigation-drawer v-model="drawer" app>
      </v-navigation-drawer>
  
      <v-main>
        <v-container fluid>
        <v-row>
          <v-col cols="12" md="6">
            <v-row>
              <v-col cols="12" md="2">
                <v-select
                  v-model="selectedLanguage1"
                  :items="languages"
                  label="Idioma"
                ></v-select>
              </v-col>
            </v-row>
              <v-row> <v-col cols="12" md="10">
                <v-textarea
                  v-model="text1"
                  label="Texto 1"
                  placeholder="Ingresa el texto 1"
                  auto-grow
                ></v-textarea>
              </v-col>
            </v-row>
          </v-col>

          <v-col cols="12" md="6">
            <v-row>
              <v-col cols="12" md="2">
                <v-select
                  v-model="selectedLanguage2"
                  :items="languages"
                  label="Idioma"
                ></v-select>
              </v-col>
            </v-row>
            <v-row>
              <v-col cols="12" md="10">
                <v-textarea
                  v-model="text2"
                  label="Texto 2"
                  placeholder="Ingresa el texto 2"
                  auto-grow
                ></v-textarea>
              </v-col>
            </v-row>
          </v-col>
        </v-row>
      </v-container>
      </v-main>
    </v-app>
  </template>
  
  <script>
  export default {
    data() {
      return {
        drawer: false,
        selectedLanguage: null,
        languages: ["Español", "Embera"], // Puedes personalizar la lista de idiomas
        text1: "",
        text2: "",
      };
    },
    methods: {
      openUserMenu() {
        this.$router.push('/login')
      },
    },
  };
  </script>
  