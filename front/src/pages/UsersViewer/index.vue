<template>
    <div>
        <h3>Users Viewer</h3>
        <b-container>
        <!-- <b-card-group deck> -->
            <b-row align-v="center">
                <user-card v-for="(user, userId) in getUsersList" :key="userId" :user="user" />
            </b-row>
        <!-- </b-card-group> -->
        </b-container>
    </div>
</template>

<script>
import UserCard from '@/components/UserCard';
import {mapGetters, mapActions} from 'vuex'
    export default {
        name: 'UsersViewer',
        components: {
            UserCard
        },
        computed: {
            ...mapGetters("users", ["getUsersList"])
        },
        methods: {
            ...mapActions("users", ["loadUsersList"])
        },
        mounted() {
            this.loadUsersList()
        }
    }
</script>

<style lang="scss" scoped>

</style>