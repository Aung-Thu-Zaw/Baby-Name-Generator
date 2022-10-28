<template>
  <div class="option-container">
    <h4>{{ option.title }}</h4>
    <div class="option-buttons">
      <button
        class="option"
        v-for="(value, index) in option.buttons"
        :key="value"
        :class="computeButtonClasses(value, index)"
        @click="options[option.category] = value"
      >
        {{ value }}
      </button>
    </div>
  </div>

  <!-- <div class="option-container">
    <h4>2) Choose the name's popularity</h4>
    <div class="option-buttons">
      <button
        class="option option-left"
        :class="{ 'option-active': options.popularity === 'Trendy' }"
        @click="options.popularity = Popularity.TRENDY"
      >
        Trendy
      </button>
      <button
        class="option option-right"
        :class="{ 'option-active': options.popularity === 'Unique' }"
        @click="options.popularity = Popularity.UNIQUE"
      >
        Unique
      </button>
    </div>
  </div>

  <div class="option-container">
    <h4>3) Choose the name's length</h4>
    <div class="option-buttons">
      <button
        class="option option-left"
        :class="{ 'option-active': options.length === 'Long' }"
        @click="options.length = Length.LONG"
      >
        Long
      </button>
      <button
        class="option"
        :class="{ 'option-active': options.length === 'All' }"
        @click="options.length = Length.ALL"
      >
        All
      </button>
      <button
        class="option option-right"
        :class="{ 'option-active': options.length === 'Short' }"
        @click="options.length = Length.SHORT"
      >
        Short
      </button>
    </div>
  </div> -->
</template>


<script setup lang="ts">
import { Gender, Length, Popularity } from "~~/data";

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

const computeButtonClasses = (value, index) => {
  const classNames = [];
  if (props.options[props.option.category] === value) {
    classNames.push("option-active");
  }
  if (index === 0) classNames.push("option-left");
  if (index === props.option.buttons.length - 1)
    classNames.push("option-right");

  return classNames.join(" ");
};
</script>

<style scoped>
.option-container {
  margin-bottom: 2rem;
}
.option {
  background-color: white;
  outline: 0.15rem solid rgb(249, 87, 89);
  border: none;
  padding: 0.75rem;
  width: 12rem;
  font-size: 1rem;
  color: rgb(27, 60, 138);
  cursor: pointer;
  font-weight: 200;
}
.option-left {
  border-radius: 1rem 0 0 1rem;
}
.option-right {
  border-radius: 0 1rem 1rem 0;
}

.option-active {
  background-color: rgb(249, 87, 89);
  color: white;
}
</style>