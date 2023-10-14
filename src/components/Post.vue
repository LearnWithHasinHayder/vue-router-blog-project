<script setup>
import { ref, onBeforeMount } from 'vue'
import { useRoute } from 'vue-router';
const route = useRoute();

const post = ref({});
const postId = route.params.id;

onBeforeMount(() => {
    fetch(`https://dummyjson.com/post/${postId}`)
        .then(res => res.json())
        .then(data => {
            post.value = data;
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
</template>
 
<style scoped></style>