<template>
  <section class="section">
    <Card />
  </section>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import Card from "./components/Card.vue";

export default defineComponent({
  name: "App",
  components: {
    Card,
  },
});
</script>

<style lang="scss">
@import "./styles/App.scss";
</style>
