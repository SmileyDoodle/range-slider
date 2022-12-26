<template>
  <div>
    <v-container
      class="main-wrapper"
      :class="[
        isAnswer === 'default'
          ? ''
          : isAnswer === 'correct'
          ? 'main-wrapper-green'
          : 'main-wrapper-red',
      ]"
    >
      <SliderPage @answer="isAnswer = $event" />
    </v-container>
  </div>
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
      isAnswer: "default" as String,
    };
  },
});
</script>
