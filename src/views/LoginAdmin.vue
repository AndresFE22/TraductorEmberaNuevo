<template>
    <v-app id="inspire">
      <div class="background">
        <v-content>
        <v-container class="fill-height" fluid >
          <v-row align="center" justify="center">
            <v-col cols="12" sm="8" md="8">
              <v-card class="elevation-12">
                <v-window v-model="step" style="padding: 10%;">
                  <v-window-item :value="1">
                    <v-row>
                      <v-col cols="12" md="8">
                        <v-card-text class="mt-12">
                          <h1
                            class="text-center display-2 teal--text text--accent-3"
                          >Sign in to Diprella</h1>
  
                          <v-form>
                            <span class="mdi mdi-account"></span>
                            <v-text-field
                              label="Usuario"
                              name="Usuario"
                              type="text"
                              color="teal accent-3"
                              v-model="username"
                            />
                            <span class="mdi mdi-lock"></span>
                            <v-text-field
                              id="password"
                              label="Contraseña"
                              name="Contraseña"
                              type="password"
                              color="teal accent-3"
                              v-model="password"
                            />
                          </v-form>
                        </v-card-text>
                        <div class="text-center mt-3">
                          <v-btn rounded color="teal accent-3" dark @click="signIn">SIGN IN</v-btn>
                        </div>
                      </v-col>
                      <v-col cols="12" md="4" class="teal accent-3">
                        <v-card-text class="white--text mt-12">
                          <h1 class="text-center display-1">Hello, Friend!</h1>
                          <h5
                            class="text-center"
                          >Enter your personal details and start journay with us</h5>
                        </v-card-text>
                      </v-col>
                    </v-row>
                  </v-window-item>
                </v-window>
              </v-card>
            </v-col>
          </v-row>
        </v-container>
      </v-content>
      </div>
    </v-app>
  </template>
  
  <script>

  export default {
    data: () => ({
      step: 1,
      username: "",
      password: ""
      
    }),
    props: {
      source: String
    },
    methods: {
    signIn() {
      // Verificar si las credenciales son correctas
      if (this.username === "admin" && this.password === "admin123") {
        // Redirigir a la ruta deseada
        this.$router.push('/panelConfiguracion');
      } else {
        // Lógica para manejar credenciales incorrectas (puedes mostrar un mensaje de error, etc.)
        console.log("Credenciales incorrectas");
      }
    },
  },
  };
  </script>

<style scoped>
.background {
background-image: url('../assets/indigena2.jpg');
background-size: cover;
height: 100vh;
}

</style>
  