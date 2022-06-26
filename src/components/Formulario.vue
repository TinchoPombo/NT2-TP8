<template>

  <section class="src-components-formulario">
    <div class="jumbotron">

      <h1>Nuevo usuario</h1>
      <hr>

      <vue-form :state="formState" @submit.prevent="enviar()">
      
        <validate tag="div">
          <label for="nombre">Nombre</label>
          <input 
            type="text"
            id="nombre"
            name="nombre"
            class="form-control"
            autocomplete="off"
            required
            :minlength="nombreMinLength"
            :maxlength="nombreMaxLength"
            v-model="$store.state.formData.nombre"
          >
          
          <field-messages name="nombre" show="$dirty">
            <div slot="required" class="alert alert-danger mt-1">
              Este campo es obligatorio.
            </div>
            <div slot="minlength" class="alert alert-danger mt-1">
                El nombre debe tener como minimo{{nombreMinLength}}  caracteres.
            </div>
            <div slot="maxlength" class="alert alert-danger mt-1">
                El nombre debe tener como maximo {{nombreMaxLength}} caracteres.
            </div>

          </field-messages>

        </validate>

        <br>

        <validate tag="div">
          <label for="edad">Edad</label>
          <input 
            type="number"
            id="edad"
            name="edad"
            class="form-control"
            v-model.number="$store.state.formData.edad"
            autocomplete="off"
            required
            :min="edadMin"
            :max="edadMax"
          >

          <field-messages name="edad" show="$dirty">
            <div slot="required" class="alert alert-danger mt-1">Este campo es obligatorio.</div>
            <div slot="min" class="alert alert-danger mt-1">La edad minima es {{edadMin}} </div>
            <div slot="max" class="alert alert-danger mt-1">La edad maxima es {{edadMax}} </div>          
          </field-messages>
        </validate>

        <br>

        <validate tag="div">
          <label for="email">Email</label>
          <input 
            type="email"
            id="email"
            name="email"
            v-model="$store.state.formData.email"
            class="form-control"
            required
            autocomplete="off"
          >

          <field-messages name="email" show="$dirty">
            <div slot="required" class="alert alert-danger mt-1">Este campo es obligatorio.</div>
            <div slot="email" class="alert alert-danger mt-1">Email invalido.</div>
          </field-messages>

          <button class="btn btn-success my-3" :disabled="formState.$invalid">Enviar</button>

        </validate>
      

      
      </vue-form>

      <br>

      <router-link to="/usuarios">
        <button type="button" class="btn btn-warning">
          Ver usuarios
        </button>
      </router-link>

    </div>
  </section>

</template>

<script>

  export default  {
    name: 'src-components-formulario',
    props: [],
    mounted () {

    },
    data () {
      return {
        formState : {},
        formData : this.getInitialData(),
        nombreMinLength : 3,
        nombreMaxLength : 15,
        edadMin : 18,
        edadMax : 120,
        personas : [],
        url : 'https://628c112fa3fd714fd02c36b5.mockapi.io/users'
      }
    },
    methods: {
      enviar(){
        this.$store.dispatch('enviarForm')
        
        this.formData = this.getInicialData()
        this.formState._reset()
      },
      getInitialData(){
        return{
          nombre : '',
          edad : '',
          email : ''
        }
      }
    },
    computed: {

    }
}


</script>

<style scoped lang="css">
  .src-components-formulario {

  }
</style>
