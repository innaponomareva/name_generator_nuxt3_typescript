<script setup lang="ts">
interface NameProps {
  name: string;
  index: number;
}
const props = defineProps<NameProps>();

const emit = defineEmits(["remove"]);

const removeName = () => {
  emit("remove", props.index);
};
</script>

<template>
  <div class="card">
    <h4>{{ name }}</h4>
    <p @click="removeName">×</p>
  </div>
</template>

<style scoped>
.card {
  margin-right: 1rem;
  margin-bottom: 0.5rem;
  background-color: rgb(27, 60, 138);
  padding: 0.1rem 1.5rem;
  color: white;
  border-radius: 1.5rem 0.5rem 1.5rem 1.5rem;
  position: relative;
}

.card p {
  position: absolute;
  top: -25%;
  right: 4%;
  color: white;
  cursor: pointer;
  padding: 0.1rem;
}
</style>
