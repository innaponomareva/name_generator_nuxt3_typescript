<script setup lang="ts">
import { Gender, Popularity, Length } from "@/data";

interface OptionProps {
  option: {
    title: string;
    category: string;
    buttons: Gender[] | Popularity[] | Length[];
  };
  options: {
    gender: Gender;
    popularity: Popularity;
    length: Length;
  };
}
const props = defineProps<OptionProps>();

const computeButtonClasses = (label, index) => {
  const classNames = [];
  if (props.options[props.option.category] === label) {
    classNames.push("option-active");
  }
  if (index === 0) {
    classNames.push("option-first");
  }
  if (index === props.option.buttons.length - 1) {
    classNames.push("option-last");
  }
  return classNames.join(" ");
};
</script>

<template>
  <div class="option-container">
    <h4>{{ option.title }}</h4>
    <div class="option-buttons">
      <Button
        v-for="(label, index) in option.buttons"
        :key="label"
        :label="label"
        type="option"
        :styles="computeButtonClasses(label, index)"
        @click="options[option.category] = label"
      />
    </div>
  </div>
</template>

<style scoped>
.option-container {
  margin-bottom: 2rem;
}
.option-buttons {
  display: flex;
  justify-content: center;
}

@media only screen and (max-width: 600px) {
  .option-buttons {
    flex-direction: column;
    align-items: center;
  }
}
</style>
