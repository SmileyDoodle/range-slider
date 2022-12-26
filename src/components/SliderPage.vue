<template>
  <div class="riddle-wrapper">
    <div v-show="isShow">
      {{ riddle }}
    </div>
  </div>
  <div class="slider-wrapper">
    <div class="amount">
      <sup>$</sup>
      <span class="dollars">{{ price }}</span>
    </div>
    <v-slider
      min="0"
      max="30"
      step="1"
      v-model="price"
      thumb-color="#EA346F"
      track-color="#2C3639"
    ></v-slider>
    <br />
    <v-btn depressed plain class="btn-submit" @click="submit()" v-if="isShow"
      >Submit</v-btn
    >
    <v-btn depressed plain class="btn-submit" @click="next()" v-if="!isShow"
      >Next</v-btn
    >
    <div class="wrong-wrapper">
      <div v-show="isWrong">Wrong answer</div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  name: "SliderPage",
  props: {
    isAnswer: {
      type: String,
      default: "default",
      required: true,
    },
  },
  data() {
    return {
      price: 15 as Number,
      index: 0 as Number,
      isShow: true as Boolean,
      isWrong: false as Boolean,
      riddles: [
        {
          question:
            "A new clothing store has a unique method of pricing items. A vest costs $20, a tie costs $15, a blouse costs $30, and underwear costs $45. How much would pants cost?" as String,
          answer: 25 as Number,
          hint: "The pricing method charges $5 for each letter needed to spell the item." as String,
        },
        {
          question:
            "A phone and case cost $110. If the phone costs $100 more than the case, how much does the case cost?" as String,
          answer: 5 as Number,
          hint: "" as String,
        },
        {
          question:
            "Aino has $29.00 dollars. She bought 4 coloring books that cost $3.00 each, and 4 boxes of crayons that cost $2.00 each. She spent the rest of her money on markers. How much money did Aino spend on markers?" as String,
          answer: 9 as Number,
          hint: "" as String,
        },
      ],
      riddle: "" as String,
    };
  },
  mounted() {
    this.init();
  },
  methods: {
    init() {
      this.riddle = this.riddles[this.index].question;
    },
    submit() {
      if (this.price === this.riddles[this.index].answer) {
        this.$emit("answer", "correct");
        this.isShow = false;
        this.isWrong = false;
      }
      if (this.price !== this.riddles[this.index].answer) {
        this.$emit("answer", "wrong");
        this.isWrong = true;
      }
    },
    next() {
      this.$emit("answer", "default");
      if (this.index === 2) {
        this.index = -1;
      }
      this.isShow = true;
      this.index++;
      this.init();
    },
  },
});
</script>
