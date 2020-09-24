<template>
  <v-layout>
    <v-flex>
      <v-form ref="form" @submit.prevent="submit">
        <v-container>
          <v-row class="ma-0 pa-0 mt-3">
            <v-col class="ma-0 pa-0">
              <span
                class="text-h5 text-left font-weight-bold pa-0 ma-0"
                style="width: 100%"
              >
                Formulario
              </span></v-col
            >
          </v-row>
          <v-row class="ma-0 pa-0">
            <v-col class="ma-0 pa-0">
              <span class="text-subtitle-1 text-left pa-0" style="width: 100%">
                Por Favor complete el siguiente formulario
              </span></v-col
            >
          </v-row>
          <v-row class="mt-6">
            <v-col cols="12" sm="12" md="6" class="ma-0 py-0">
              <v-text-field
                v-model="form.nombre"
                outlined
                required
                clearable
                :rules="rules.nombre"
                background-color="#f5f5f5"
              >
                <div slot="label">
                  <span class="labelCustom">Nombres *</span>
                </div>
              </v-text-field>
            </v-col>
          </v-row>
          <v-row>
            <v-col cols="12" sm="12" md="6" class="ma-0 py-0">
              <v-text-field
                v-model="form.direccion"
                outlined
                required
                clearable
                background-color="#f5f5f5"
              >
                <div slot="label">
                  <span class="labelCustom">Dirección</span>
                </div>
              </v-text-field>
            </v-col>
          </v-row>
          <v-row>
            <v-col cols="12" sm="12" md="6" class="ma-0 py-0 pb-0">
              <v-select
                v-model="form.genero"
                background-color="#f5f5f5"
                :items="items"
                outlined
              >
                <div slot="label">
                  <span class="labelCustom">Género</span>
                </div>
              </v-select>
            </v-col>
          </v-row>
          <v-row class="ma-0 pa-0">
            <v-col class="ma-0 pa-0" cols="12" sm="12" md="6">
              <span
                class="text-subtitle-1 text-left pa-0 ma-0"
                style="width: 100%"
              >
                * Campos requeridos
              </span></v-col
            >
          </v-row>
          <v-row class="ma-0 pa-0 mt-2">
            <v-col class="ma-0 pa-0" cols="12" sm="12" md="6">
              <v-btn
                ripple
                height="60px"
                x-large
                block
                dark
                :disabled="!formIsValid"
                class="boton"
                type="submit"
                ><span class="text-h5 font-weight-bold">Enviar</span></v-btn
              >
            </v-col>
          </v-row>
        </v-container>
      </v-form>
    </v-flex>
  </v-layout>
</template>

<script>
import Swal from 'sweetalert2'

export default {
  components: {},
  data() {
    const defaultForm = Object.freeze({
      nombre: '',
      direccion: '',
      genero: '',
    })
    return {
      form: Object.assign({}, defaultForm),
      items: ['Hombre', 'Mujer', 'No Binario'],
      rules: {
        nombre: [(val) => (val || '').length > 0 || 'Este campo es requerido'],
      },
      defaultForm,
    }
  },
  computed: {
    formIsValid() {
      return this.form.nombre
    },
  },
  methods: {
    submit() {
      if (this.$refs.form.validate()) {
        this.$axios
          .put('https://postman-echo.com/put', {
            name: this.form.nombre,
            email: this.form.direccion,
            gender: this.form.genero,
          })
          .then((response) => {
            Swal.fire(
              `Hola! ${this.form.nombre}`,
              'Tus datos fueron grabados con exito',
              'success'
            )
            this.$refs.form.reset()
          })
          .catch((err) => {
            Swal.fire('Error!', 'No se pudo guardar la información', 'error')
            console.log(err)
          })
      }
    },
  },
}
</script>
<style lang="scss">
$text-field-outlined-fieldset-border-width: 0px !important;
$text-field-outlined-fieldset-border: 0px solid currentColor !important;

.labelCustom {
  font-weight: bold;
  color: black;
}

.boton {
  background: rgb(107, 115, 255);
  background: linear-gradient(
    356deg,
    rgba(107, 115, 255, 1) 0%,
    rgba(0, 212, 255, 1) 100%
  );
}
.theme--light.v-app-bar.v-toolbar.v-sheet {
  background-color: #ffffff;
}

.v-input__slot > fieldset {
  border: none;
}
</style>
