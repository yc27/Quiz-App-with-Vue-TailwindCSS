<template>
  <nav class="flex flex-wrap justify-center bg-teal-500 p-6 m-0">
    <div class="flex w-full items-center justify-center text-blue-900 mb-2">
      <svg
        class="fill-current h-8 w-8 mr-2"
        width="54"
        height="54"
        viewBox="0 0 54 54"
        xmlns="http://www.w3.org/2000/svg"
      >
        <path
          d="M13.5 22.1c1.8-7.2 6.3-10.8 13.5-10.8 10.8 0 12.15 8.1 17.55 9.45 3.6.9 6.75-.45 9.45-4.05-1.8 7.2-6.3 10.8-13.5 10.8-10.8 0-12.15-8.1-17.55-9.45-3.6-.9-6.75.45-9.45 4.05zM0 38.3c1.8-7.2 6.3-10.8 13.5-10.8 10.8 0 12.15 8.1 17.55 9.45 3.6.9 6.75-.45 9.45-4.05-1.8 7.2-6.3 10.8-13.5 10.8-10.8 0-12.15-8.1-17.55-9.45-3.6-.9-6.75.45-9.45 4.05z"
        />
      </svg>
      <span class="font-semibold text-2xl tracking-tight">Fancy Quiz App</span>
    </div>

    <div class="flex w-full items-center justify-center">
      <span class="text-pink-900 font-semibold mr-2">Counter:</span>
      <span class="text-xl text-gray-900">{{ numCorrect }}/{{ numTotal }}</span>
    </div>
  </nav>
</template>

<script>
export default {
  name: "Nav",
  props: {
    numCorrect: Number,
    numTotal: Number,
  },
};
</script>

<style scoped>
nav {
  margin: 0 !important;
}
</style>