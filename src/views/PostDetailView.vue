<template>
    <div class="container">
        <div>
            <h1>{{ post.id + "- " + post.title }}</h1>
            <p>{{ post.body }}</p>
            <!-- <img :src="post.url"> -->
        </div>
        <router-link :to="{name: 'PostList'}">Volver atrás</router-link>
    </div>
</template>

<script setup>
    import { onMounted } from 'vue'
    import { useRoute } from 'vue-router'
    import PostService from '@/services/PostService';

    const service = new PostService()
    const post = service.getPost()
    
    onMounted( async() => {
        const route = useRoute()
        const element = route.params.id
        await service.fetchById(element)
    })
</script>

<style scoped>
</style>