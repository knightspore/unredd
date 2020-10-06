<template>
    <!-- Feed Post -->
    <div class="m-4 flex flex-col justify-between bg-white bg-opacity-25 rounded-lg shadow-md">
        <!-- Title + Info -->
        <div class="p-4 grid gap-2">
            <a class="text-sm font-bold text-gray-500" :href="'https://reddit.com/r/' + post.subreddit" target="_blank">/r/{{post.subreddit}}</a>
            <h2 class="text-lg">{{post.title}}</h2>
            <a class="text-sm text-gray-500" :href="'https://reddit.com/u/' + post.author" target="_blank">Post by {{post.author}}</a>
        </div>
        <!-- Link + NSFW Warning -->
        <div class="p-2 font-bold">
            <a :href="'https://reddit.com' + post.permalink" target="_blank" class="flex justify-end items-center gap-x-2"><p v-if="post.over_18" class="text-sm text-red-500">NSFW!</p><svg class="w-4 h-4" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg"><path fill-rule="evenodd" d="M10.293 3.293a1 1 0 011.414 0l6 6a1 1 0 010 1.414l-6 6a1 1 0 01-1.414-1.414L14.586 11H3a1 1 0 110-2h11.586l-4.293-4.293a1 1 0 010-1.414z" clip-rule="evenodd"></path></svg></a>
        </div>
    </div>
</template>

<script>
import axios from 'axios'

export default {
    name: 'RedditPost',
    props: [
        'post'
    ],
    data () {
        return {
            downvotes: null,
        }
    },
    mounted () {
        this.downvotes = Math.floor( this.post.ups - (this.post.ups * this.post.upvote_ratio));
    }
}
</script>