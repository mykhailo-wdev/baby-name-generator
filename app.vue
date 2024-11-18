<template>
  <div class="container">
    <h1>Baby Name Generator</h1>
    <p>Chooshe your option and click the "Find Names" buttom below</p>
    <div class="options-container">
      <Option 
        v-for="option in optionsArray" :key="option.title" 
        :option="option"
        :options="options"
         />
      <button class="primary" @click="cumputeSelectedNames">Find Names</button>
      <div class="cards-container">
        <CardName 
          v-for="(name, idx) in selectedNames" :key="name" 
          class="card" 
          :name="name" 
          @remove="() => removeName(idx)"
          :idx='idx'
          />
      </div>
    </div>
  </div>
</template>


<script setup lang="ts">
import { Gender, Popularity, Length, names } from "@/data"

interface OptionsState {
  gender: Gender,
  popularity: Popularity,
  length: Length
}

 const options = reactive<OptionsState>({
  gender: Gender.GIRL,
  length: Length.SHORT,
  popularity: Popularity.TRENDY
})

const cumputeSelectedNames = () => {
  const filterNames = names
  .filter((name) => name.gender === options.gender)
  .filter((name) => name.popularity === options.popularity)
  .filter((name) => {
    if(options.length === Length.ALL) return true
    else {
      return name.length === options.length
    }
  })

  selectedNames.value = filterNames.map(name => name.name)
}

const selectedNames = ref<string[]>([])

const removeName = (idx: number) => {
  const filteredNames = [...selectedNames.value]
  filteredNames.splice(idx, 1)
  selectedNames.value = filteredNames
}

const optionsArray: Array<{
  title: string;
  category: "gender" | "popularity" | "length";
  buttons: Gender[] | Popularity[] | Length[];
}> = [
  {
    title: "1) Choose a gender",
    category: "gender",
    buttons: [Gender.GIRL, Gender.BOY, Gender.UNISEX]
  },
  {
    title: "2) Choose the name's popularity",
    category: "popularity",
    buttons: [Popularity.UNIQUE, Popularity.TRENDY]
  },
  {
    title: "3) Choose name's length",
    category: "length",
    buttons: [Length.SHORT, Length.ALL, Length.LONG]
  }
];


</script>


<style scoped>
.container {
  font-family: Arial, Helvetica, sans-serif;
  color: rgb(27, 60, 138);
  max-width: 50rem;
  margin: 0 auto;
  text-align: center;
}

h1 {
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
  cursor: pointer;
  background-color: rgb(249, 87, 89);
  color: rgb(255, 255, 255);
  border: none;
  outline: none;
  padding: 0.7rem 4rem;
  font-size: 1rem;
  margin-top: 1rem;
  border-radius: 6.5rem;
}

.cards-container {
  display: flex;
  margin-top: 3rem;
  flex-wrap: wrap;
}
</style>
