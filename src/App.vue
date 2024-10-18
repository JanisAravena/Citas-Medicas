<template>
  <div class="bg-cover bg-center min-h-screen flex items-center justify-center" style="background-image: url('https://static.vecteezy.com/system/resources/previews/006/429/746/large_2x/abstract-background-gradient-abstract-modern-background-for-mobile-apps-free-vector.jpg');">
    <div class="container mx-auto p-6 bg-white shadow-lg rounded-lg flex">
      <!-- Imagen del Doctor -->
      <div class="w-1/3 flex justify-center items-center">
        <img class="w-64" src="https://static.vecteezy.com/system/resources/previews/022/484/658/non_2x/cute-doctor-women-compassionate-and-skilled-models-for-medical-industry-projects-transparent-background-free-png.png" alt="Doctor cartoon" />
      </div>

      <!-- Formulario de Citas -->
      <div class="w-2/3 flex flex-col items-center">
        <h1 class="text-3xl font-bold mb-6 text-center">Administrador de Citas Médicas</h1>
        <form @submit.prevent="agregarCita" class="space-y-4 w-full max-w-md">
          <div v-for="(input, key) in formFields" :key="key" class="flex flex-col">
            <label :class="{'text-red-500': input.valor === '', 'text-black': input.valor !== '', 'font-bold': true}">{{ input.label }}</label>
            <input
              v-if="input.type !== 'select'"
              v-model="input.valor"
              :type="input.type"
              :placeholder="input.label"
              class="border rounded p-2 border-gray-300"
            />
            <select
              v-else
              v-model="input.valor"
              class="border rounded p-2 border-gray-300"
            >
              <option value="" disabled>Selecciona la gravedad</option>
              <option value="baja">Baja</option>
              <option value="media">Media</option>
              <option value="alta">Alta</option>
            </select>
          </div>
          <div class="flex justify-center mt-4">
            <button :disabled="!formularioCompleto" class="bg-blue-500 text-white px-4 py-2 rounded disabled:opacity-50">Agregar Cita</button>
          </div>
        </form>

        <!-- Mensaje si no hay citas -->
        <p v-if="citas.length === 0" class="mt-4 text-center">Aún no hay consultas registradas</p>

        <!-- Lista de Citas -->
        <div v-for="(cita, index) in citas" :key="index" class="mt-4 w-full max-w-md">
          <CitaCard :cita="cita" @eliminarCita="eliminarCita(index)" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import CitaCard from './components/CitaCard.vue';

export default {
  data() {
    return {
      citas: [],
      formFields: {
        paciente: { label: 'Paciente', valor: '', type: 'text' },
        fecha: { label: 'Fecha', valor: '', type: 'date' },
        hora: { label: 'Hora', valor: '', type: 'time' },
        gravedad: { label: 'Gravedad', valor: '', type: 'select' },
        motivo: { label: 'Motivo', valor: '', type: 'text' },
      },
    };
  },
  computed: {
    formularioCompleto() {
      return Object.values(this.formFields).every(field => field.valor !== '');
    },
  },
  methods: {
    agregarCita() {
      const nuevaCita = {
        paciente: this.formFields.paciente.valor,
        fecha: this.formFields.fecha.valor,
        hora: this.formFields.hora.valor,
        gravedad: this.formFields.gravedad.valor,
        motivo: this.formFields.motivo.valor,
      };
      this.citas.push(nuevaCita);
      Object.values(this.formFields).forEach(field => (field.valor = ''));
    },
    eliminarCita(index) {
      this.citas.splice(index, 1);
    },
  },
  components: {
    CitaCard,
  },
};
</script>

<style scoped>
.container {
  max-width: 900px;
}
</style>