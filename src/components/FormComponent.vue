<!-- Inputs de formulario -->
<template>
  <!--  Evita que la pagina se recargue en cambio llama a el metodo agregar cita -->
  <form @submit.prevent="agregarCita" class="form-container">
    <div>
      <!--  La :class permite marcar en rojo la label del input esperando que ingrese toda la información -->
      <label :class="{ invalid: !paciente }">Paciente</label>
      <!-- El @input verifica cada entreda de datos validando  el formulario  -->
      <input type="text" v-model="paciente" @input="validateForm">
    </div>
    <div>
      <label :class="{ invalid: !fecha }">Fecha</label>
      <input type="date" v-model="fecha" @input="validateForm">
    </div>
    <div>
      <label :class="{ invalid: !hora }">Hora</label>
      <input type="time" v-model="hora" @input="validateForm">
    </div>
    <div>
      <label :class="{ invalid: !gravedad }">Gravedad</label>
      <select v-model="gravedad" @input="validateForm">
        <option value="Default">Seleccione...</option>
        <option value="Baja">Baja</option>
        <option value="Media">Media</option>
        <option value="Alta">Alta</option>
      </select>
    </div>
    <div>
      <label :class="{ invalid: !motivo }">Motivo</label>
      <input type="text" v-model="motivo" @input="validateForm">
    </div>
    <div>
      <!-- Permite que el boton este deshabilitado esperando que se validen todos los campos-->
      <button type="submit" :disabled="!isFormValid">Agregar</button>
    </div>
  </form>

</template>

<script>
export default {
  data() {
    return {
      paciente: '',
      fecha: '',
      hora: '',
      gravedad: '',
      motivo: '',
      isFormValid: false,
    };
  },
  methods: {
  // < !--Permite validar que se rellenen los campos solicitados en el formulario -- >
  validateForm() {
  this.isFormValid = this.paciente && this.fecha && this.hora && this.gravedad && this.motivo;
},
  // < !--Este método crea un objeto con los datos del formulario-- >
  agregarCita() {
  const cita = {
    paciente: this.paciente,
    fecha: this.fecha,
    hora: this.hora,
    gravedad: this.gravedad,
    motivo: this.motivo
  };
  // <!--Emite un evento con datos del formulario -->
  this.$emit('agendarCita', cita);
  // <!--Limpia los campos del formulario -->
  this.limpiarFormulario();
},
limpiarFormulario() {
  this.paciente = "";
  this.fecha = "";
  this.hora = "";
  this.gravedad = "";
  this.motivo = "";
  this.isFormValid = "";
}
  }
};
</script>

<style>
.form-container {
  border: 1px solid #ccc;
  padding: 15px;
  border-radius: 5px;
  display: flex;
  justify-content: row;
  gap: 10px;
}

label {
  display: block;
  margin-bottom: 5px;
  color: black;
}

.invalid {
  color: red;
}

input,
select {
  width: 100%;
  padding: 8px;
  box-sizing: border-box;
}

button:disabled {
  background-color: #ccc;
  cursor: not-allowed;
}

button {
  width: 100%;
  padding: 10px;
  margin-top: 10px;
  background-color: #4CAF50;
  color: white;
  border: none;
  cursor: pointer;
  font-size: 16px;
}
</style>
