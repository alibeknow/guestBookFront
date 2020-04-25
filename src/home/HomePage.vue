<template>
    <div>
        <h1>Hi {{user.username}}!</h1>
        <p>You're logged in with Vue + Vuex & JWT!!</p>
        <h3>Users from secure api end point:</h3>
        <em v-if="users.loading">Loading users...</em>
        <span v-if="users.error" class="text-danger">ERROR: {{users.error}}</span>
        <ul v-if="user">
            <li v-for="item in user.items" :key="item.id">
                {{item.username + ' ' + item.id}}
                <span v-if="item.deleting"><em> - Deleting...</em></span>
                <span v-else-if="item.deleteError" class="text-danger"> - ERROR: {{item.deleteError}}</span>
                <span v-else> - <a @click="deleteUser(item.id)" class="text-danger">Delete</a></span>
            </li>
        </ul>
        <p>
            <router-link to="/login">Logout</router-link>
        </p>
    </div>
</template>

<script>
import { mapState, mapActions } from 'vuex'

export default {
    computed: {
        ...mapState({
            account: state => state.account,
            users: state => state.users.all
        })
    },
    created () {
        this.getAllUsers();
    },
    methods: {
        ...mapActions('users', {
            getAllUsers: 'getAll',
            deleteUser: 'delete'
        })
    }
};
</script>