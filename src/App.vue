<template>
  <div id="app" class="bg-gray-300 h-screen">
    <Nav class="mb-6" :numCorrect="numCorrect" :numTotal="numTotal" />

    <QuestionBox
      v-if="fetchComplete"
      :index="index"
      :currentQuestion="questions[index]"
      :next="next"
      :increment="increment"
    />

    <p
      v-if="!fetchComplete"
      class="text-center text-3xl font-bold text-red-600 py-16"
    >Fetching Data...</p>
  </div>
</template>

<script>
import Nav from "./components/Nav.vue";
import QuestionBox from "./components/QuestionBox.vue";

export default {
  name: "App",
  components: {
    Nav,
    QuestionBox,
  },
  data() {
    return {
      fetchComplete: false,
      questions: [],
      index: 0,
      numCorrect: 0,
      numTotal: 0,
    };
  },
  methods: {
    next() {
      this.index++;
    },
    increment(isCorrect) {
      if (isCorrect) {
        this.numCorrect++;
      }
      this.numTotal++;
    },
  },
  mounted: function () {
    fetch("https://opentdb.com/api.php?amount=10&category=27&type=multiple", {
      method: "get",
    })
      .then((response) => {
        return response.json();
      })
      .then((jsonData) => {
        this.questions = jsonData.results;
        this.fetchComplete = true;
      });
  },
};
</script>

<style>
.btn-disabled,
.btn-disabled:hover {
  background: #bdbcbc !important ;
}
</style>
