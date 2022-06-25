<template>

  <section class="src-components-usuarios">
    <div class="jumbotron">
    
      <h1>Usuarios</h1>
      <hr>

      <div v-if="this.$store.state.usuarios.length" class="table-responsive">
        <table class="table table-dark">
          <tr>
            <th>Nombre</th>
            <th>Edad</th>
            <th>Email</th>
          </tr>
          <tr v-for="(usuario, index) in this.$store.state.usuarios" :key="index">
            <td> {{ usuario.nombre }} </td>
            <td> {{ usuario.edad }} </td>
            <td> {{ usuario.email }} </td>
          </tr>
        </table>
      </div>
        <h5 v-else class="alert alert-danger">
          No se encontraron usuarios
        </h5>
    
    </div>

  </section>

</template>

<script>

  export default  {
    name: 'src-components-usuarios',
    props: [],
    mounted () {

    },
    created () {
      this.getUsuarios()
    },
    data () {
      return {
        url: 'https://628c112fa3fd714fd02c36b5.mockapi.io/users'
      }
    },
    methods: {
      async getUsuarios(){
        this.$store.dispatch('getUsuarios')
      }
    },
    computed: {

    }
}


</script>

<style scoped lang="css">
  .src-components-usuarios {

  }
</style>
