<script>
import Card from "./Card.vue";

export default {
  name: "CardGrid",
  components: { Card },
  props: {
    students: {
      type: Array,
      required: true,
    },
  },
};
</script>

<template>
  <div class="w-full bg-blue-300 border-blue-200 border-8 p-4 rounded-xl">
    <ul
      class="grid grid-cols-1 gap-6 md:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4"
    >
      <li v-for="student in students" :key="student.id" class="h-full">
        <Card :student="student" />
      </li>
    </ul>
  </div>
</template>