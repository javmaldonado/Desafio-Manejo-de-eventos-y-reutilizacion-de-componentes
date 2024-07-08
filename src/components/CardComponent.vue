<!--  Crear la card que se imprimira con el contenido solicitado -->
<template>
    <!--  Agregar la :class para determinar el color de la card según la gravedad del paciente -->
    <div class="card"
        :class="{ 'gravedadBaja': cita.gravedad === 'Baja', 'gravedadMedia': cita.gravedad === 'Media', 'gravedadAlta': cita.gravedad === 'Alta' }">
        <p><strong>Paciente:</strong> {{ cita.paciente }}</p>
        <p><strong>Fecha:</strong> {{ cita.fecha }}</p>
        <p><strong>Hora:</strong> {{ cita.hora }}</p>
        <p><strong>Gravedad:</strong> {{ cita.gravedad }}</p>
        <p><strong>Motivo:</strong> {{ cita.motivo }}</p>
        <!--  Emit recibe un string con nombre de un evento que se declara al padre "App" -->
        <button @click="$emit('eliminarCita')" class="buttonEliminar">Eliminar</button>
    </div>
</template>

<script>
export default {
    props: {
        cita: {}
    },
    // <!-- Permite eliminar la card" -->
    methods: {
        eliminarCita() {
            this.$emit('eliminar-cita');
        },
    },
};
</script>

<style>
.card {
    background-color: #ffffcc;
    border: 1px solid #6c6c61;
    padding: 15px;
    border-radius: 5px;
    margin-bottom: 10px;
    display: inline-block;
    justify-content: row;
    width: 15%;

}

.buttonEliminar {
    background-color: crimson;
    color: white;
    border: none;
    padding: 5px 10px;
    cursor: pointer;
}


.gravedadBaja {
    background-color: lightgreen;
}

.gravedadMedia {
    background-color: rgb(252, 252, 181);
}

.gravedadAlta {
    background-color: rgb(239, 133, 133);
}
</style>