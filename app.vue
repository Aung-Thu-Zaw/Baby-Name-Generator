<template>
  <div class="container">
    <h1>Baby Name Generator</h1>
    <p>Choose Your options and click the "Find Names" button below</p>
    <div class="options-container">
      <div class="option-container">
        <h4>1) Choose a gender</h4>
        <div class="option-buttons">
          <button
            class="option option-left"
            :class="{ 'option-active': options.gender === 'Boy' }"
            @click="options.gender = Gender.BOY"
          >
            Boy
          </button>
          <button
            class="option"
            :class="{ 'option-active': options.gender === 'Unisex' }"
            @click="options.gender = Gender.UNISEX"
          >
            Unisex
          </button>
          <button
            class="option option-right"
            :class="{ 'option-active': options.gender === 'Girl' }"
            @click="options.gender = Gender.GIRL"
          >
            Girl
          </button>
        </div>
      </div>
      <div class="option-container">
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
      </div>
      <button class="primary" @click="computeSelectedNames">Find Names</button>
    </div>

    <div class="card-container">
      <div class="card" v-for="name in selectedNames" :key="name">
        <h4>
          {{ name }}
        </h4>
        <p>x</p>
      </div>
    </div>
  </div>

  <!-- <div>
    {{ options.gender }}
    <br />
    {{ options.length }}
    <br />
    {{ options.popularity }}
    <br />
    {{ selectedNames }}
  </div> -->
</template>

<script setup lang="ts">
import { Gender, Popularity, Length, names } from "@/data";

//Interface is give a pair of key and type
// Define Specifi key in our object contains
interface OptionsState {
  gender: Gender;
  popularity: Popularity;
  length: Length;
}

// const obj: OptionsState = {
//   gender: Gender.GIRL,
//   length: Length.SHORT,
//   popularity: Popularity.UNIQUE,
// };

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

// This array needed only name string
const selectedNames = ref<string[]>([]);

console.log("this is a selected names:", selectedNames);
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
.card {
  background-color: rgb(27, 60, 138);
  width: 28%;
  color: white;
  border-radius: 1rem;
  padding: 0.1rem;
  margin-right: 0.5rem;
  margin-bottom: 1rem;
  position: relative;
}
.card p {
  position: absolute;
  top: -15%;
  left: 90%;
  cursor: pointer;
  color: rgba(255, 255, 255, 0.178);
}
</style>