<script>
import CardGrid from "./components/CardGrid.vue";

export default {
  name: "App",
  components: { CardGrid },
  data() {
    return {
      studentsData: [
        {
          id: 1,
          name: "Jordi",
          surname: "Matorrales",
          age: 25,
          penColor: "negro",
        },
        {
          id: 2,
          name: "Sergi",
          surname: "Pérez Olivé",
          age: 50,
          penColor: "azul",
        },
        {
          id: 3,
          name: "Maria Elena",
          surname: "Sánchez",
          age: 50,
          penColor: "azul",
        },
      ],
      newStudent: { name: "", surname: "", age: "", penColor: "" },
    };
  },
  methods: {
    addStudent() {
      if (
        !this.newStudent.name ||
        !this.newStudent.surname ||
        !this.newStudent.age
      )
        return;

      this.studentsData.push({
        id: this.studentsData.length + 1,
        ...this.newStudent,
        age: Number(this.newStudent.age),
      });
      this.newStudent = { name: "", surname: "", age: "", penColor: "" };
    },
  },
  computed: {
    studentsWithoutBluePen() {
      let count = 0;
      for (const student of this.studentsData) {
        if (student.penColor != "azul") count++;
      }
      return count;
    },
  },
};
</script>

<template>
  <div
    class="mx-auto container flex flex-col items-start justify-start w-full min-h-screen text-left"
  >
    <h1 class="text-4xl font-bold text-blue-500 mb-8">Estudiantes de Merit School</h1>

    <h2>Lista actual de alumnos que asisten al exámen</h2>
    <CardGrid :students="studentsData" />

    <section class="flex flex-col mt-16">
      <h2>Formulario de ingreso de alumnos</h2>
      <form @submit.prevent="addStudent">
        <!-- Ya ves en este contexto prevent no me confunde T_T -->

        <div class="flex gap-4 mb-8 flex-wrap">
          <!-- Field Name  -->
          <div class="flex flex-col">
            <label for="newStudent.name" class="text-gray-700"
              >Nombre <span class="text-red-500 font-black">*</span></label
            >
            <input
              v-model="newStudent.name"
              placeholder="Pedro"
              class="bg-gray-400 placeholder-gray-500 text-black border p-2 rounded-lg shadow-inner shadow-gray-500"
              required
            />
          </div>

          <!-- Surname Field -->
          <div class="flex flex-col">
            <label for="newStudent.surname" class="text-gray-700"
              >Apellido(s) <span class="text-red-500 font-black">*</span></label
            >
            <input
              v-model="newStudent.surname"
              placeholder="García"
              class="bg-gray-400 placeholder-gray-500 text-black border p-2 rounded-lg shadow-inner shadow-gray-500"
              required
            />
          </div>

          <!-- Surname Age -->
          <div class="flex flex-col">
            <label for="newStudent.age" class="text-gray-700"
              >Edad <span class="text-red-500 font-black">*</span></label
            >
            <input
              v-model="newStudent.age"
              placeholder="18"
              min="18"
              class="bg-gray-400 placeholder-gray-500 text-black border p-2 rounded-lg shadow-inner shadow-gray-500 w-24"
              required
            />
          </div>

          <!-- Pen Colour (blue is approved for exam!) -->
          <div class="flex flex-col">
            <label for="newStudent.penColor" class="text-gray-700"
              >Color de bolígrafo</label
            >
            <input
              v-model="newStudent.penColor"
              placeholder="azul"
              class="bg-gray-400 placeholder-gray-500 text-black border p-2 rounded-lg shadow-inner shadow-gray-500"
            />
          </div>
        </div>

        <button
          type="submit"
          class="bg-blue-600 text-white w-48 px-4 py-2 rounded-lg hover:bg-blue-500 shadow-inner shadow-gray-200"
        >
          Agregar estudiante
        </button>
      </form>
    </section>

    <section class="flex flex-col mt-16">
      <h2>Alerta de faltantes de bolígrafos azules</h2>
      <p class="font-bold text-red-500">Alumnos sin bolígrafo azul: {{ studentsWithoutBluePen }}</p>

    </section>
  </div>
</template>
