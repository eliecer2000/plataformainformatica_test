<template>
  <v-layout class="fondo">
    <v-flex class="text-center pt-10 mt-10">
      <v-avatar color="primary" size="160">
        <img
          src="https://joeschmoe.io/api/v1/random"
          class="borderImg"
          onerror="if (this.src != 'user.svg') this.src = 'user.svg';"
        />
      </v-avatar>
      <v-row class="ma-0 pa-0 mt-3">
        <v-col class="ma-0 pa-0">
          <span
            class="text-h5 text-left font-weight-bold pa-0 ma-0"
            style="width: 100%"
          >
            {{ usuario.nombre }}
          </span></v-col
        >
      </v-row>
      <v-row class="ma-0 pa-0 mt-3 text-center">
        <v-col class="ma-0 pa-0">
          <span class="group pa-2 text-center">
            <v-avatar size="30" class="mx-3">
              <img src="~/assets/linkedin.svg" />
            </v-avatar>
            <v-avatar size="30" class="mx-3">
              <img src="~/assets/twitter.svg" />
            </v-avatar>
            <v-avatar size="30" class="mx-3">
              <img src="~/assets/facebook.svg" />
            </v-avatar>
          </span>
        </v-col>
      </v-row>
    </v-flex>
    <overlay :status="loading" />
  </v-layout>
</template>
<script>
import Swal from 'sweetalert2'
import overlay from './../components/overlay'
export default {
  name: 'Index',
  components: {
    overlay,
  },
  data() {
    return {
      loading: true,
      usuario: {
        nombre: null,
        redes: {
          linkedin: '',
          twitter: '',
          facebook: '',
        },
        avatar: null,
      },
      dialogStatus: false,
    }
  },
  mounted() {
    this.consultarUsuario()
  },
  methods: {
    usuarioActual() {
      const min = 1
      const max = 10
      return Math.floor(Math.random() * (max - min + 1)) + min
    },
    async consultarUsuario() {
      try {
        this.loading = true
        const usuarioSeleccionado = await this.usuarioActual()
        const datosUsuario = await this.$axios.$get(
          `https://jsonplaceholder.typicode.com/users/${usuarioSeleccionado}`
        )
        this.usuario.nombre = datosUsuario.name
        this.loading = false
      } catch (e) {
        this.loading = false
        Swal.fire({
          title: 'Error!',
          text: 'No se puede consultar los datos del usuario',
          icon: 'error',
          confirmButtonText: 'OK',
        })
        // console.log(e)
      }
    },
  },
}
</script>
<style lang="scss">
.borderImg {
  border: 5px solid #b8b8b8;
}
</style>
