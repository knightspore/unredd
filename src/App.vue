<template>
  <main class="antialiased min-h-screen bg-gray-100" :class="{ 'text-gray-100 bg-gray-900': darkmode }">
  <span class="m-6 absolute right-0 top-0" @click="toggleDarkmode()"><svg class="m-auto w-6 h-6" :class="{ 'text-gray-100' : darkmode }" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg"><path d="M11 3a1 1 0 10-2 0v1a1 1 0 102 0V3zM15.657 5.757a1 1 0 00-1.414-1.414l-.707.707a1 1 0 001.414 1.414l.707-.707zM18 10a1 1 0 01-1 1h-1a1 1 0 110-2h1a1 1 0 011 1zM5.05 6.464A1 1 0 106.464 5.05l-.707-.707a1 1 0 00-1.414 1.414l.707.707zM5 10a1 1 0 01-1 1H3a1 1 0 110-2h1a1 1 0 011 1zM8 16v-1h4v1a2 2 0 11-4 0zM12 14c.015-.34.208-.646.477-.859a4 4 0 10-4.954 0c.27.213.462.519.476.859h4.002z"></path></svg></span>

  <!-- Header -->
  <header class="p-8 text-center grid gap-2">
  <h1 class="font-bold uppercase text-2xl">Unredd</h1>
  <p>reddit without distractions</p>
  </header>

  <Feed :darkmode="darkmode"/>

  </main>
</template>

<script>
import Feed from './components/Feed.vue'

export default {
  name: 'App',
  components: {
    Feed,
  },
  data () {
    return {
      darkmode: false,
    }
  },
  mounted () {
    if (localStorage.darkmode) {
      this.darkmode = localStorage.darkmode;
    }
  },
  methods: {
    toggleDarkmode() {
      this.darkmode = !this.darkmode,
      localStorage.darkmode = this.darkmode
    }
  }
}
</script>

<style>
.fade-enter-active, .fade-leave-active {
  transition: opacity 1s ease;
}
.fade-enter, .fade-leave-to {
  opacity: 0;
}
</style>