<template>
    <div class="w-96 mx-auto">

        <Stat :stats="statistics"/>

        <h1 class="mb-8 pb-8 border-b border-b-gray-400 text-2xl">Posts</h1>
        <div v-if="posts">
            <Post v-for="post in posts" :post="post"></Post>
        </div>
    </div>
</template>

<script>
import Post from '../../components/Post.vue'
import Stat from '../../components/Stat.vue'

export default {
    name: "Personal",
    data () {
        return {
            statistics: [],
            posts: [],
            userId: this.$route.params.id,

        }
    },

    components: {
        Post,
        Stat,
    },

    mounted () {
        this.getPosts()
        this.getStats()
    },

    methods: {

        getStats() {
            axios.post('/api/users/stats',{user_id: this.userId})
                .then(res => {
                    this.statistics = res.data.data

                    console.log(res)
                })
        },

        getPosts() {
            axios.get(`/api/users/${this.userId}/posts`)
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
