<script setup>
import { ref, onBeforeMount } from 'vue'
import { useRoute } from 'vue-router'
import axios from 'axios'
const route = useRoute()

const skip = ref(20)

const posts = ref([])
onBeforeMount(() => {
    // fetch('https://dummyjson.com/posts?limit=20')
    //     .then(res => res.json())
    //     .then(data => {
    //         posts.value = data.posts
    //     })

    axios.get('https://dummyjson.com/posts?limit=20')
        .then(res => {
            posts.value = res.data.posts
        })
})

function loadMorePosts() {
    // fetch(`https://dummyjson.com/posts?limit=20&skip=${skip.value}`)
    //     .then(res => res.json())
    //     .then(data => {
    //         posts.value = [...posts.value, ...data.posts]
    //         skip.value += 20
    //     })
    axios.get(`https://dummyjson.com/posts?limit=20&skip=${skip.value}`)
        .then(res => {
            posts.value = [...posts.value, ...res.data.posts]
            skip.value += 20
        })
}
</script>
 
<template>
    <div class="my-5">
        <!-- {{ posts }} -->
    </div>
    <article v-for="post in posts" class="mb-10">
        <router-link :to="{ name: 'post', params: { id: post.id } }">
            <h1 class="text-xl mb-2">{{ post.title }}</h1>
            <p>
                <img :src="`//source.unsplash.com/random/300x200?${post.id}`" :alt="post.title">
            </p>
        </router-link>
        <p>
            {{ post.body }}
        </p>
    </article>
    <div class="my-5" v-show="posts.length>0">
        <button @click="loadMorePosts()" class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded">
            Load More
        </button>
    </div>
</template>
 
<style scoped></style>