<script setup>
import { ref, onBeforeMount } from 'vue'
import { useRoute } from 'vue-router';
import axios from 'axios';
const route = useRoute();

const post = ref({});
const postId = route.params.id;

const comments = ref([])

onBeforeMount(() => {
    // fetch(`https://dummyjson.com/post/${postId}`)
    //     .then(res => res.json())
    //     .then(data => {
    //         post.value = data;
    //     })
    axios.get(`https://dummyjson.com/post/${postId}`)
        .then(res => {
            post.value = res.data;
        })

    axios.get(`https://dummyjson.com/post/${postId}/comments`)
        .then(res => {
            comments.value = res.data.comments;
        })


})

</script>
 
<template>
    <article class="mb-10">
        <h1 class="text-xl mb-2">{{ post.title }}</h1>
        <p>
            <img :src="`//source.unsplash.com/random/300x200?${post.id}`" :alt="post.title">
        </p>
        <p>
            {{ post.body }}
        </p>
    </article>
    <article class="" v-show="comments.length>0">
        <h2 class="font-bold underline-gray-600 mb-2">Comments</h2>
        <hr>
        <ul class="mt-5">
            <li v-for="comment in comments" :key="comment.id">
                <p>
                    <strong>{{ comment.user.username }}</strong> said <em>{{ comment.body }}</em>
                </p>
            </li>
        </ul>
    </article>
</template>
 
<style scoped></style>