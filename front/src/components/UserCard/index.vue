<template>
  <div>
    <b-col>
      <b-card>
        <b-card-body>
          <b-card-title>{{user.firstName }} {{user.lastName}}</b-card-title>
          <b-card-sub-title class="mb-2"><b-icon-at />{{user.email}}</b-card-sub-title>
          <b-card-sub-title class="mb-2"><b-icon-phone />{{user.phoneNumber}}</b-card-sub-title>
          <b-card-text><b-icon-house-door />{{user.address}}</b-card-text>
          <b-button-group class="mx-1">
            <b-button variant="outline-primary" v-b-tooltip.hover title="Edit user" :to="`users/${user._id}`">Edit</b-button>
            <b-button variant="outline-danger" v-b-tooltip.hover title="Delete user" @click="deleteUser(user._id)">Delete</b-button>
          </b-button-group>
        </b-card-body>
      </b-card>
    </b-col>
  </div>
</template>

<script>
import { mapActions } from 'vuex'

export default {
  name: 'UserCard',
  props: {
    user: {
      type: Object,
      required: true
    }
  },
  methods: {
    ...mapActions("users", ["deleteUser"])
  }
}
</script>

<style scoped></style>
