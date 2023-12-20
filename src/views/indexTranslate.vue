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
          <v-row></v-row>
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
                  v-model="texto"
                  placeholder="Traduce aqui"
                  auto-grow
                  @input="reiniciarTemporizador"
                  ></v-textarea>
              </v-col>
            </v-row>
          </v-col>

          <v-btn icon @click="intercambiarIdiomas">
        <v-icon>mdi-swap-horizontal</v-icon>
      </v-btn>
  
          
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
                  disabled
                  label="Traducción"
                  v-model="translate"
                  placeholder="Traducción"
                  auto-grow
                ></v-textarea>
              </v-col>
            </v-row>
          </v-col>
        </v-row>
        <button @click="traducir" >Traducir</button>
      </v-container>
      </v-main>
    </v-app>
  </template>
  
  <script>
import axios from 'axios'
export default {
    data() {
      return {
        drawer: false,
        selectedLanguage1: "Español",
        selectedLanguage2: "Embera",
        languages: ["Español", "Embera"], 
        texto: "",
        translate: "",
        temporizador: null
      };
    },
    methods: {
      openUserMenu() {
        this.$router.push('/login')
      },

      reiniciarTemporizador() {
        clearTimeout(this.temporizador);
        this.temporizador = setTimeout(() => {
          this.traducir();
        }, 1000)  
      },

      traducir() {
        const paquete = 
        {
      idiom1: this.selectedLanguage1,
      idiom2: this.selectedLanguage2,
      texto: this.texto,}

        axios.post(`http://127.0.0.1:5000//translate`, {paquete: paquete}) 
        .then(response => {
          this.translate = response.data.translate
          console.log(this.translate)
        })
        .catch(error => {
          console.error(error);
        });
      },
      intercambiarIdiomas() {
      const temp = this.selectedLanguage1;
      this.selectedLanguage1 = this.selectedLanguage2;
      this.selectedLanguage2 = temp;

      const tempTexto = this.texto;
      this.texto = this.translate;
      this.translate = tempTexto;
    }
    },
  };
  </script>

  <style></style>
  