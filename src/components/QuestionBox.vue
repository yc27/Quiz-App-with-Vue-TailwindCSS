<template>
  <div class="flex flex-wrap justify-center py-6 px-4">
    <div class="w-full md:w-1/2 lg:w-1/3 border border-gray-500 rounded py-2">
      <div class="w-full">
        <span class="flex justify-end pr-3">{{index+1}}/10</span>
        <p class="text-center font-bold text-lg p-4 pt-3">{{ currentQuestion.question }}</p>
      </div>

      <ul class="w-full list-none divide-y-2 divide-gray-500 divide-dashed">
        <li
          v-for="(answer, index) in shuffledAnswers"
          :key="index"
          @click.prevent="selectAnswer(index)"
          :class="answerClass(index)"
          class="px-4 py-2 hover:bg-blue-200 hover:text-gray-900 cursor-pointer"
        >{{ answer }}</li>
      </ul>
    </div>

    <div class="w-full flex justify-center py-4">
      <button
        @click="submitAnswer"
        :disabled="selectedIndex === null || answered"
        :class="[selectedIndex === null || answered ? 'btn-disabled' : '']"
        class="bg-blue-600 hover:bg-blue-700 px-4 py-2 mr-4 text-gray-100 font-bold rounded"
      >Submit</button>

      <button
        @click="next"
        :disabled="index === 9"
        :class="[index === 9? 'btn-disabled' : '']"
        class="bg-green-600 hover:bg-green-700 px-4 py-2 text-gray-100 font-bold rounded"
      >Next</button>
    </div>
  </div>
</template>

<script>
import _ from "lodash";

export default {
  props: {
    index: Number,
    currentQuestion: Object,
    next: Function,
    increment: Function,
  },
  data: function () {
    return {
      selectedIndex: null,
      correctIndex: null,
      shuffledAnswers: [],
      answered: false,
    };
  },
  watch: {
    currentQuestion: {
      immediate: true,
      handler() {
        this.selectedIndex = null;
        this.answered = false;
        this.shuffleAnswers();
      },
    },
  },
  methods: {
    selectAnswer(index) {
      this.selectedIndex = index;
    },
    submitAnswer() {
      let isCorrect = false;

      if (this.selectedIndex === this.correctIndex) {
        isCorrect = true;
      }
      this.answered = true;

      this.increment(isCorrect);
    },
    shuffleAnswers() {
      let answers = [
        ...this.currentQuestion.incorrect_answers,
        this.currentQuestion.correct_answer,
      ];
      this.shuffledAnswers = _.shuffle(answers);
      this.correctIndex = this.shuffledAnswers.indexOf(
        this.currentQuestion.correct_answer
      );
    },
    answerClass(index) {
      let answerClass = "";

      if (!this.answered && this.selectedIndex === index) {
        answerClass = "bg-blue-300";
      } else if (this.answered && this.correctIndex === index) {
        answerClass = "bg-green-500 text-gray-100";
      } else if (
        this.answered &&
        this.selectedIndex === index &&
        this.correctIndex !== index
      ) {
        answerClass = "bg-red-500 text-gray-100";
      }

      return answerClass;
    },
  },
};
</script>
