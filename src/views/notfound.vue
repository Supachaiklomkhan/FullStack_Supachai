<template>
  <div class="flex flex-col items-center justify-center w-full h-screen bg-gray-100 px-10">
    <h1 class="text-[12rem] font-extrabold text-gray-800 mb-6">404</h1>
    <p class="text-2xl text-gray-600 mb-8">
      The page you're looking for doesn't exist.
    </p>
    <button
      @click="goHome"
      class="px-8 py-4 bg-blue-600 text-white rounded-lg hover:bg-blue-700 transition-colors duration-200 text-lg font-semibold"
    >
      Go to Home
    </button>
  </div>
</template>

<script>
export default {
  name: "NotFound",
  methods: {
    goHome() {
      this.$router.push('/');
    },
  },
};
</script>
