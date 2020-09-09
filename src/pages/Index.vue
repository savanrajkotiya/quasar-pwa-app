<template>
  <div class="flex flex-center">
    <div class="row justify-center full-width q-pa-lg">
      <q-btn
        @click="generateBoard"
        label="generate board"
        color="grey-7"
        size="lg"
      />
    </div>
    <div class="row q-pa-sm q-col-gutter-xs">
      <div v-for="(word, index) in generatedwords" class="col-3" :key="index">
        <q-btn
          :label="word.word"
          :color="word.color"
          class="full-width q-pa-sm"
          unelevated
        />
      </div>
    </div>
  </div>
</template>

<script>
import words from "../assets/words.js";
export default {
  name: "OneWord",
  data() {
    return {
      words,
      generatedwords: []
    };
  },
  methods: {
    generateBoard() {
      this.generatedwords = [];
      let random = [];

      while (random.length < 16) {
        let r = this.words[Math.floor(Math.random() * this.words.length)];
        if (random.indexOf(r) === -1) {
          random.push(r); // unique words push every time
        }
      }

      let newarray = [];

      random.map(obj => {
        newarray.push({
          word: obj,
          color: ""
        });
      });

      newarray.map(obj => {
        if (newarray.filter(v => v.color === "green-7").length < 5) {
          obj.color = "green-7";
        } else if (newarray.filter(v => v.color === "blue-7").length < 5) {
          obj.color = "blue-7";
        } else if (newarray.filter(v => v.color === "grey-7").length < 5) {
          obj.color = "grey-7";
        } else {
          obj.color = "dark";
        }
      });

      this.generatedwords = [];
      this.generatedwords = this.shuffle(newarray);
      console.log(this.generatedwords);
    },
    // shuffle an array randomly
    shuffle(a) {
      for (let i = a.length - 1; i > 0; i--) {
        const j = Math.floor(Math.random() * (i + 1));
        [a[i], a[j]] = [a[j], a[i]];
      }
      return a;
    }
  }
};
</script>
