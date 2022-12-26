<template>
  <v-container class="main-wrapper">
    <SliderPage />
  </v-container>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import SliderPage from "./components/SliderPage.vue";

export default defineComponent({
  name: "App",

  components: {
    SliderPage,
  },

  data() {
    return {
      //
    };
  },
});
</script>
