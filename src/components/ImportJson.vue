<template>
  <div>
    <h2>Student List:</h2>
    <ul>
      <li v-for="student in studentList" :key="student.id">
        {{ student.firstName }} {{ student.lastName }}
      </li>
    </ul>
    <h2>Behavior:</h2>
    <ul>
      <li v-for="b in behavior" :key="b.id">
        {{ b.name }}: {{ b.Score }}
        </li>
    </ul>
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";

let studentList = ref([]);
let behavior = ref([]);

onMounted(() => {
  fetch("https://dummyjson.com/users?limit=10")
    .then((res) => res.json())
    .then((data) => {
      studentList.value = data.users.map((student) => ({
        id: student.id,
        firstName: student.firstName,
        lastName: student.lastName,
      }));
    });

  import("../assets/behavior.json")
    .then((module) => {
      behavior.value = module.default;
    })
});
</script>

<style>
</style>