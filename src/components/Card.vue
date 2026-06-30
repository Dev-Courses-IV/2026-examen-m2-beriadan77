<script>
export default {
  name: "Card",
  computed: {
    penColorIcon() {
      if (this.student.penColor === "azul") return "🔵";
      else if (this.student.penColor === "rojo") return "🔴";
      else if (this.student.penColor === "verde") return "🟢";
      else if (this.student.penColor === "negro") return "⚫️";
      else return "❌";
    },
  },
  props: {
    student: {
      type: Object,
      required: true,
    },
  },
};
</script>

<template>
  <div
    class="flex flex-col border border-blue-400 rounded-lg w-full h-full shadow-md"
    :class="student.penColor === 'azul' ? 'bg-blue-200' : 'bg-red-300'"
  >
    <h2
      class="font-bold p-2"
      :class="
        student.penColor === 'azul'
          ? 'text-blue-950 bg-blue-500'
          : 'text-red-950 bg-red-500'
      "
    >
      {{ student.name }} {{ student.surname }}
    </h2>
    <div class="p-2">
      <p class="font-semibold text-gray-700">Age: {{ student.age }}</p>
      <p class="font-semibold text-gray-700">Pen color {{ penColorIcon }}</p>
      <p class="font-semibold text-gray-500">Student ID: {{ student.id }}</p>
    </div>
  </div>
</template>
