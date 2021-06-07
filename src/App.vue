<template>
  <Pronunciation />
</template>

<script lang="ts">
import { defineComponent } from "vue";
import Pronunciation from "./components/Pronunciation.vue";

export default defineComponent({
  name: "App",
  components: {
    Pronunciation,
  },
});
</script>

<style></style>
