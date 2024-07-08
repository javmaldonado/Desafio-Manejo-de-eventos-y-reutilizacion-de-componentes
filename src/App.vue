<template>
  <div id="app">
    <h1>Citas Médicas</h1>
    <!--  Traer datos del formulario hijo agregar citas -->
    <FormComponent @agendarCita="agendarCita" />
    <!--  v-if muestra el contenido solo cuando hay citas registradas -->
    <div class="citas-container" v-if="citas.length > 0">
      <!--  Traer datos del la card hijo eliminar citas -->
      <CardComponent v-for="(cita, index) in citas" :key="index" :cita="cita" @eliminarCita="eliminarCita(index)" />
    </div>
    <p class="registroCitas" v-else> Aún no hay citas registradas</p>
  </div>
</template>

<!--  Importante importar los componentes hijos al padre "App" -->
<script>
import FormComponent from './components/FormComponent.vue';
import CardComponent from './components/CardComponent.vue';

export default {
  name: 'App',
  components: {
    FormComponent,
    CardComponent,
  },
  data() {
    return {
      citas: [],
    };
  },
  methods: {
    // <!--  Añade citas  -->
    agendarCita(cita) {
      this.citas.push(cita);
    },
    // <!--  Elimina citas  -->
    eliminarCita(index) {
      this.citas.splice(index, 1);
    }
  }
};
</script>

<style>
body {
  font-family: Arial, sans-serif;
  padding: 20px;
}

.registroCitas {
  color: red;
  text-align: center;
}

.citas-container {
  display: inline-block;
  margin-top: 20px;
  gap: 20px;
}

h1 {
  text-align: center;
}

.card-container {
  margin-top: 20px;
}
</style>
