<template>
  <div>
    <h3>User Editor</h3>
    <b-form >
      <div class="text-center" v-if="isLoading">
        <b-spinner variant="primary"></b-spinner>
      </div>
      <b-form-group id="input-group-1" label="User first name:" label-for="input-1">
        <b-form-input id="input-1" v-model="firstName" required placeholder="Enter first name"></b-form-input>
      </b-form-group>

      <b-form-group id="input-group-2" label="User last name:" label-for="input-2">
        <b-form-input id="input-2" v-model="lastName" required placeholder="Enter last name"></b-form-input>
      </b-form-group>
      
      <b-form-group id="input-group-3" label="Email address:" label-for="input-3">
        <b-form-input id="input-3" v-model="email" type="email" required placeholder="Enter user email"></b-form-input>
      </b-form-group>

      <b-form-group id="input-group-4" label="Phone number:" label-for="input-4">
        <b-form-input id="input-4" v-model="phoneNumber" type="tel" required placeholder="Enter user phone number"></b-form-input>
      </b-form-group>

      <b-form-group id="input-group-5" label="Address:" label-for="input-5">
        <b-form-input id="input-5" v-model="address" type="text" required placeholder="Enter user address"></b-form-input>
      </b-form-group>

      <b-button variant="outline-success" :disabled="!isDataValid" @click="saveUser">{{ saveBtnTitle }}</b-button>
      <b-button variant="outline-danger" @click="onCancel">Cancel</b-button>
    </b-form>
  </div>
</template>

<script>
import { mapActions, mapGetters } from 'vuex';
export default {
  name: "UserEditor",
  data() {
      return {
          firstName: null,
          lastName: null,
          email: null,
          phoneNumber: null,
          address: null
      }
  },
  computed: {
      ...mapGetters("users", ["getUserToUpdate", "isLoading"]),

      userId() {
          return this.$route.params.userId 
      },
      isDataValid() {
          return (this.firstName && this.lastName && this.email && this.phoneNumber && this.address)
      },
      saveBtnTitle() {
          return this.userId ? "Save" : "Add"
      }
  },
  watch: {
      isLoading(newValue) {
        if (!newValue) {
          const userToUpdate = this.getUserToUpdate
            this.firstName = userToUpdate.firstName,
            this.lastName = userToUpdate.lastName,
            this.email = userToUpdate.email,
            this.phoneNumber = userToUpdate.phoneNumber,
            this.address = userToUpdate.address
        }
      }
  },
  methods: {
      ...mapActions("users", ["addUser", "updateUser", "findUserById"]),

      saveUser() {
          if (this.userId) {
              this.updateUser({
                    _id: this.userId,
                    firstName: this.firstName,
                    lastName: this.lastName,
                    email: this.email,
                    phoneNumber: this.phoneNumber,
                    address: this.address
              })
           } else {
               this.addUser({
                    firstName: this.firstName,
                    lastName: this.lastName,
                    email: this.email,
                    phoneNumber: this.phoneNumber,
                    address: this.address})
           }
        this.$router.push({path: "/users"})
      },
      onCancel() {
          this.$router.push({path: "/users"})
      }
  },
  created() {
      if (this.userId) {
          this.findUserById(this.userId)
          
          }
  }
};
</script>

<style lang="scss" scoped>
</style>