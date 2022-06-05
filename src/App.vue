<template>
  <section class="section">
    <div class="container">
      <div class="switch__row">
        <span class="switch__info">Show cats</span>
        <button>All or Cats</button>
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
        <div class="output" v-for="(animal, index) in animals" :key="animal.id">
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
  </section>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import HelloWorld from "./components/HelloWorld.vue";

type Breed = "cat" | "dog";

type Animal = {
  id: number;
  name: string;
  breed: Breed;
};

export default defineComponent({
  name: "App",
  // components: {
  //   HelloWorld,
  // },
  data: () => ({
    inputValue: "",
    filter: "all",
    breed: "",
    animals: [] as Animal[],
  }),
  methods: {
    firstCharUpper(str: string) {
      return str.charAt(0).toUpperCase() + str.slice(1);
    },
    toUpper(str: string) {
      return str.toUpperCase();
    },
    add() {
      this.animals.push({
        id: Math.random(),
        name: this.inputValue,
        breed: this.breed as Breed,
      });
      this.inputValue = "";
      this.breed = "";
    },
    deleteAnimal(index: number) {
      this.animals.splice(index, 1);
    },
  },
});
</script>

<style lang="scss">
@import "./styles/App.scss";
@import "./styles/Form.scss";
</style>
