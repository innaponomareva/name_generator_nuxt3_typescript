<script setup lang="ts">
interface ButtonProps {
  label: string;
  type: "primary" | "option";
  styles?: string;
}
const props = defineProps<ButtonProps>();

const computeClasses = () => {
  const classNames = [];
  if (props.type === "primary") {
    classNames.push("primary");
  }
  if (props.type === "option") {
    classNames.push("option");
  }
  if (props.styles) {
    classNames.push(props.styles);
  }
  return classNames.join(" ");
};
</script>
<template>
  <button :class="computeClasses()">{{ label }}</button>
</template>

<style>
.primary {
  width: 30%;
  background-color: rgb(249, 87, 89);
  color: white;
  border-radius: 2rem;
  border: none;
  padding: 0.75rem 4rem;
  font-size: 1rem;
  margin-top: 1rem;
  cursor: pointer;
}

.option {
  background-color: white;
  outline: 0.1rem solid rgb(27, 60, 138);
  border: none;
  padding: 0.75rem;
  width: 20%;
  font-size: 1rem;
  color: rgb(27, 60, 138);
  cursor: pointer;
  font-weight: 200;
}
.option-first {
  border-radius: 2rem 0 0 2rem;
}
.option-last {
  border-radius: 0 2rem 2rem 0;
}

.option-active {
  background-color: rgb(27, 60, 138);
  color: white;
}

@media only screen and (max-width: 600px) {
  .primary,
  .option {
    width: 40%;
    display: flex;
    justify-content: center;
    margin: 0 auto;
  }
  .option-first {
    border-radius: 2rem 2rem 0 0;
  }
  .option-last {
    border-radius: 0 0 2rem 2rem;
  }
}
</style>
