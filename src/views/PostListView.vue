<template>
    <div class="container">
        <h1>Listado de Posts</h1>
        <ul class="postList">
            <li v-for="post in posts" :key="post.id">
                <router-link class="routerLink" :to="{name: 'PostDetail', params: {id:post.id}}">
                    {{ post.id + ". " + post.title }}
                </router-link>
            </li>
        </ul>
    </div>
</template>

<script lang="js" setup>
    import { onMounted } from 'vue'
    import PostService from '@/services/PostService';
    const service = new PostService()
    const posts = service.getPosts()

    onMounted( async() => {
        await service.fetchAll()
    })
</script>

<style lang="scss" scoped>
    .postList{
        width: 95vw;
        height: 75px;
        list-style-type: none;
        
        li{
            width: 95%;
            padding: 10px;
            border: 1px solid #ccc;
            color: #2c3e50;
            cursor: pointer;

            .routerLink{
                color: #2c3e50;
                text-decoration: none;
            }

            .routerLink:hover{
                color: white;
            }
        }

        li:hover{
            color: white;
            background-color: #2c3e50;
        }
    }
</style>