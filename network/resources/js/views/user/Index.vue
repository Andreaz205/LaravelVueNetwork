<template>
    <div class="w-96 mx-auto">
        <div v-if="users">
            <div class="flex justify-between items-center mb-6 pb-6 border-b border-gray-200" v-for="user in users">
                <router-link :to="{name: 'user.show', params: {id: user.id}}">
                    <p>{{ user.id }}</p>
                    <p>{{ user.name }}</p>
                    <p>{{ user.email }}</p>
                </router-link>
                <div>
                    <a
                        href="#"
                        :class="['block w-32 p-2 text-center text-sm rounded-3xl', user.is_followed ? 'bg-white text-sky border border-sky-500' : 'bg-sky-500 text-white']"
                        @click.prevent="toggleFollowing(user)"
                    >
                        {{ user.is_followed ? 'Unsubscribe' : 'Subscribe'  }}
                    </a>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import axios from "axios";

export default {
    name: "Index",

    data() {
        return {
            users: []
        }
    },

    mounted() {
        this.getUsers()
    },

    methods: {
        getUsers(){
            axios.get('/api/users')
                .then(res => {
                    this.users = res.data.data
                    console.log(res.data)
                })
        },

        toggleFollowing(user){
            axios.post(`/api/users/${user.id}/toggle_following`)
                .then(res => {
                    user.is_followed = res.data.is_followed
                    console.log(res.data.is_followed)
                })
        }
    }
}
</script>

<style scoped>

</style>
