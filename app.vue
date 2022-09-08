<script setup lang="ts">
import { Gender, Popularity, Length, names, optionsArray } from "@/data";

interface OptionsState {
  gender: Gender;
  popularity: Popularity;
  length: Length;
}

const options: OptionsState = reactive({
  gender: Gender.GIRL,
  popularity: Popularity.UNIQUE,
  length: Length.LONG,
});

const selectedNames = ref<string[]>([]);

const removeName = (index: number) => {
  const filteredNames = [...selectedNames.value];
  filteredNames.splice(index, 1);
  selectedNames.value = filteredNames;
};

const computeSelectedNames = () => {
  const filteredNames = names
    .filter((name) => name.gender === options.gender)
    .filter((name) => name.popularity === options.popularity)
    .filter((name) => {
      if (options.length === Length.ALL) return true;
      else return name.length === options.length;
    });
  selectedNames.value = filteredNames.map((name) => name.name);
};
</script>

<template>
  <div>
    <div class="container">
      <h1>Name Generator</h1>
      <div>Define your options and click the "Find" button</div>
      <div class="options-container">
        <Option
          v-for="option in optionsArray"
          :key="option.title"
          :option="option"
          :options="options"
        />
        <Button label="Find" type="primary" @click="computeSelectedNames" />
      </div>
      <div class="cards-container">
        <CardName
          v-for="(name, index) in selectedNames"
          :key="name"
          :name="name"
          @remove="() => removeName(index)"
          :index="index"
        />
      </div>
    </div>
  </div>
</template>

<style scoped>
.container {
  font-family: Arial, Helvetica, sans-serif;
  color: rgb(27, 60, 138);
  max-width: 50rem;
  margin: 0 auto;
  text-align: center;
}
.container h1 {
  font-size: 3rem;
}
.options-container {
  width: 90%;
  margin: 3rem auto;
  position: relative;
  background-color: rgb(255, 238, 236);
  border-radius: 1em;
  padding: 1rem 1rem 2.5rem;
}

.cards-container {
  display: flex;
  margin: 3rem auto 0;
  flex-wrap: wrap;
  justify-content: center;
  width: 50%;
}

@media only screen and (max-width: 600px) {
  .container h1 {
    font-size: 2rem;
  }
}
</style>
