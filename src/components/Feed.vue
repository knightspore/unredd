<template>
  <div>

    <!-- Search -->
    <div class="flex justify-center items-center gap-4">
      <form @submit.prevent="refreshSearch()" class="p-2 flex justify-center">
        <div class="flex items-center px-4 py-2 font-bold text-gray-100 rounded-full shadow-inner" :class="{'bg-gray-700': darkmode, 'bg-gray-900': !darkmode}">
          <input class="bg-transparent" type="text" v-model="subreddit" placeholder="Subreddit...">
          <button type="submit">
            <svg class="m-auto w-6 h-6 fill-current" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg"><path d="M9 9a2 2 0 114 0 2 2 0 01-4 0z"></path><path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm1-13a4 4 0 00-3.446 6.032l-2.261 2.26a1 1 0 101.414 1.415l2.261-2.261A4 4 0 1011 5z" clip-rule="evenodd"></path></svg>
          </button>
        </div>
      </form>
    </div>

		<!-- Loading Spinner -->
    <transition name="fade">
      <div class="flex h-64 items-center justify-center" v-if="loading">
          <svg class="w-12 h-12 m-auto animate-spin" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg"><path fill-rule="evenodd" d="M10 2a1 1 0 011 1v1a1 1 0 11-2 0V3a1 1 0 011-1zm4 8a4 4 0 11-8 0 4 4 0 018 0zm-.464 4.95l.707.707a1 1 0 001.414-1.414l-.707-.707a1 1 0 00-1.414 1.414zm2.12-10.607a1 1 0 010 1.414l-.706.707a1 1 0 11-1.414-1.414l.707-.707a1 1 0 011.414 0zM17 11a1 1 0 100-2h-1a1 1 0 100 2h1zm-7 4a1 1 0 011 1v1a1 1 0 11-2 0v-1a1 1 0 011-1zM5.05 6.464A1 1 0 106.465 5.05l-.708-.707a1 1 0 00-1.414 1.414l.707.707zm1.414 8.486l-.707.707a1 1 0 01-1.414-1.414l.707-.707a1 1 0 011.414 1.414zM4 11a1 1 0 100-2H3a1 1 0 000 2h1z" clip-rule="evenodd"></path></svg>
      </div>
    </transition>

    <!-- Feed -->
    <div v-if="!loading">
      <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3">
        <RedditPost v-for="post in redditPosts" :key="post.id" :post="post.data"/>
      </div>
    </div>

  </div>
</template>

<script>
import axios from 'axios'
import RedditPost from './RedditPost.vue'

export default {
  components: {
    RedditPost,
  },
  props: [
    'darkmode'
  ],
  data() {
    return {
      redditPosts: null,
      loading: true,
      subreddit: '',
    }
  },
  mounted() {
    this.loading = true;
    axios.get('https://reddit.com/' + this.subreddit + '.json').then(response => {
      this.redditPosts = response.data.data.children;
      this.loading = false;
    }).catch(error => {
      console.log(error);
      this.loading = false;
    })
  },
  methods: {
    refreshSearch() {
      this.showErrorMessage = false;
      this.loading = true;
      this.redditPosts = null;
      axios.get('https://www.reddit.com/r/' + this.subreddit + '.json').then(response => {
        this.redditPosts = response.data.data.children;
        this.loading = false;
      }).catch(error => {
        console.log(error);
        this.showErrorMessage = true;
        this.loading = false;
      })
    }
  }
}
</script>