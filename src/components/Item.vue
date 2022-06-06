<template>
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
</template>

<script lang="ts">
import { defineComponent } from "vue";

type Breed = "cat" | "dog";

type Animal = {
  id: number;
  name: string;
  breed: Breed;
};

// export default defineComponent({
//   name: "ItemComponent",
//   emits: [deleteAnimal],
//   data: () => ({
//     animals: [] as Animal[],
//   }),
//   methods: {
//     deleteAnimal(index) {
//       this.$emit("deleteAnimal", index);
//     },
//   },
// });
</script>

<style scoped lang="scss">
@import "../styles/Item.scss";
</style>
