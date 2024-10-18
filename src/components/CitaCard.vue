<template>
    <div :style="estiloDeGravedad" class="cita-card flex flex-col items-center">
      <img src="https://img.icons8.com/emoji/48/000000/face-with-medical-mask.png" alt="Sick emoji" class="mb-2"/>
      <p><strong>Paciente:</strong> {{ cita.paciente }}</p>
      <p><strong>Fecha:</strong> {{ cita.fecha }}</p>
      <p><strong>Hora:</strong> {{ cita.hora }}</p>
      <p><strong>Motivo:</strong> {{ cita.motivo }}</p>
      <button @click="eliminarCita" class="mt-2">Eliminar</button>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      cita: Object,
    },
    computed: {
      estiloDeGravedad() {
        let color;
        switch (this.cita.gravedad.toLowerCase()) {
          case 'alta':
            color = '#ffcccc'; // Suave rojo
            break;
          case 'media':
            color = '#fff3cd'; // Suave amarillo
            break;
          case 'baja':
            color = '#d4edda'; // Suave verde
            break;
          default:
            color = 'white';
        }
        return { backgroundColor: color };
      },
    },
    methods: {
      eliminarCita() {
        this.$emit('eliminarCita');
      },
    },
  };
  </script>
  
  <style scoped>
  .cita-card {
    padding: 1rem;
    margin-bottom: 1rem;
    border: 1px solid #ccc;
    border-radius: 4px;
    text-align: center;
  }
  button {
    background-color: #6c757d; /* Gris */
    color: white;
    padding: 0.5rem;
    border: none;
    cursor: pointer;
    border-radius: 4px;
  }
  button:hover {
    background-color: #5a6268; /* Gris oscuro */
  }
  </style>