<script setup>
import { ref, onBeforeMount } from 'vue'
import { useRoute } from 'vue-router'
const route = useRoute()

const posts = ref([])
onBeforeMount(() => {
    fetch('https://dummyjson.com/posts?limit=20')
        .then(res => res.json())
        .then(data => {
            posts.value = data.posts
        })
})
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
</template>
 
<style scoped></style>