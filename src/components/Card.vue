<template>
  <div class="container">
    <div class="switch__row">
      <span class="switch__info">{{
        viewMode === "all" ? "Show cats" : "Show all"
      }}</span>
      <button @click="toggleView()">All or Cats</button>
    </div>
    <h1 class="title">Cats vs Dogs</h1>
    <form class="form" @submit.prevent="add()">
      <input
        class="input"
        type="text"
        v-model="inputValue"
        placeholder="Add new animal..."
        autofocus
        required="required"
      />
      <select class="select" v-model="breed" required>
        <option value="" hidden selected>Choose breed</option>
        <option value="cat">CAT</option>
        <option value="dog">DOG</option>
      </select>
      <button class="button__add">
        <span>ADD</span>
      </button>
    </form>
    <div class="result">
      <div
        class="output"
        v-for="(animal, index) in animalsView"
        :key="animal.id"
      >
        <!--        <Item />-->
        <div class="output__row">
          <span class="breed">{{ toUpper(animal.breed) }}</span>
          <span>{{ firstCharUpper(animal.name) }}</span>
        </div>
        <div class="buttonsBox">
          <button class="button__remove" @click="deleteAnimal(index)">
            <svg
              xmlns="http://www.w3.org/2000/svg"
              width="24"
              height="24"
              style="fill: rgba(255, 255, 255, 1)"
            >
              <path
                d="M6 7H5v13a2 2 0 0 0 2 2h10a2 2 0 0 0 2-2V7H6zm10.618-3L15 2H9L7.382 4H3v2h18V4z"
              ></path>
            </svg>
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import Item from "./components/Item.vue";

type Breed = "cat" | "dog";

type ViewMode = "all" | "cats";

type Animal = {
  id: number;
  name: string;
  breed: Breed;
};

export default defineComponent({
  name: "CardComponent",
  components: {
    // Item,
  },
  data: () => ({
    inputValue: "",
    viewMode: "all" as ViewMode,
    breed: "",
    animals: [] as Animal[],
  }),
  created() {
    // const storageAnimals = JSON.parse(localStorage.getItem("animals" || "[]");
    // this.animals = storageAnimals;
  },
  computed: {
    animalsView() {
      if (this.viewMode === "cats") {
        return this.cats;
      }
      return this.animals;
    },
    cats() {
      return this.animals.filter((animal) => animal.breed === "cat");
    },
  },
  methods: {
    firstCharUpper(str: string) {
      return str.charAt(0).toUpperCase() + str.slice(1);
    },
    toUpper(str: string) {
      return str.toUpperCase();
    },
    add() {
      const newAnimals = [...this.animals];
      newAnimals.push({
        id: Math.random(),
        name: this.inputValue,
        breed: this.breed as Breed,
        // localStorage.setItem('animals', JSON.stringify(this.animals))
      });
      this.inputValue = "";
      this.breed = "";
      this.animals = newAnimals;
    },
    deleteAnimal(index: number) {
      const newAnimals = [...this.animals];
      newAnimals.splice(index, 1);
      this.animals = newAnimals;
    },
    toggleView() {
      if (this.viewMode === "all") {
        this.viewMode = "cats";
      } else {
        this.viewMode = "all";
      }
    },
  },
  // watch: {
  //   animals(newAnimals) {
  //     localStorage.setItem("animals", JSON.stringify(newAnimals));
  //   },
  // },
});
</script>

<style scoped lang="scss">
@import "../styles/Card.scss";
</style>
