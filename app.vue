<template>
  <div class="container">
    <h1>Baby Name Generator</h1>
    <p>Choose Your options and click the "Find Names" button below</p>
    <div class="options-container">
      <Option
        v-for="option in optionsArray"
        :key="option.title"
        :option="option"
        :options="options"
      />
      <button class="primary" @click="computeSelectedNames">Find Names</button>
    </div>

    <div class="card-container">
      <CardName
        v-for="(name, index) in selectedNames"
        :key="name"
        :name="name"
        :index="index"
        @remove="() => removeName(index)"
      />
    </div>
  </div>
</template>

<script setup lang="ts">
import { Gender, Popularity, Length, names } from "@/data";

interface OptionsState {
  gender: Gender;
  popularity: Popularity;
  length: Length;
}

const options = reactive<OptionsState>({
  gender: Gender.GIRL,
  length: Length.SHORT,
  popularity: Popularity.UNIQUE,
});

const computeSelectedNames = () => {
  const filterNames = names
    .filter((name) => name.gender === options.gender)
    .filter((name) => name.popularity === options.popularity)
    .filter((name) => {
      if (options.length === Length.ALL) return true;
      else return name.length === options.length;
    });

  selectedNames.value = filterNames.map((name) => name.name);
};

const selectedNames = ref<string[]>([]);

const optionsArray = [
  {
    title: "1) Choose a gender",
    category: "gender",
    buttons: [Gender.GIRL, Gender.UNISEX, Gender.BOY],
  },
  {
    title: "2) Choose the name's popularity",
    category: "popularity",
    buttons: [Popularity.TRENDY, Popularity.UNIQUE],
  },
  {
    title: "3) Choose name's length",
    category: "length",
    buttons: [Length.SHORT, Length.ALL, Length.LONG],
  },
];

const removeName = (index: number) => {
  const filteredNames = [...selectedNames.value];
  filteredNames.splice(index, 1);
  selectedNames.value = filteredNames;

};
</script>

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
  background-color: rgb(255, 238, 236);
  border-radius: 2rem;
  padding: 1rem;
  width: 95%;
  margin: 0 auto;
  margin-top: 4rem;
  position: relative;
}

.primary {
  background-color: rgb(249, 87, 89);
  color: white;
  border-radius: 6.5rem;
  border: none;
  padding: 0.75rem 4rem;
  font-size: 1rem;
  margin-top: 1rem;
  cursor: pointer;
}

.card-container {
  display: flex;
  margin-top: 3rem;
  flex-wrap: wrap;
}
</style>