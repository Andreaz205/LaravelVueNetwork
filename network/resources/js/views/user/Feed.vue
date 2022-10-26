<template>
    <div class="w-96 mx-auto">
        <h1 class="mb-8 pb-8 border-b border-b-gray-400 text-2xl">Posts</h1>
        <div v-if="posts.length">
            <div v-for="post in posts">
                <Post :post="post"></Post>
            </div>
        </div>
    </div>
</template>

<script>
import Post from '../../components/Post.vue'

export default {
    name: "Feed",
    data () {
        return {
            posts: [],
        }
    },

    components: {
      Post
    },

    mounted () {
        this.getPosts()
    },

    methods: {
        getPosts() {
            axios.get(`/api/users/following_posts`)
                .then(res => {
                    this.posts = res.data.data
                    console.log(res)
                })
        },
    }
}
</script>

<style scoped>

</style>
