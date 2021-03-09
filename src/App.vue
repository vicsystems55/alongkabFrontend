<template>
  <v-app>
    <v-app-bar
      app
      color="primary"
      dark
    >
      <div class="d-flex align-center">
        <v-img
          alt="Vuetify Logo"
          class="shrink mr-2"
          contain
          src="https://cdn.vuetifyjs.com/images/logos/vuetify-logo-dark.pn"
          transition="scale-transition"
          width="40"
        />

        <v-img
          alt="Vuetify Name"
          class="shrink mt-1 hidden-sm-and-down"
          contain
          min-width="100"
          src="https://cdn.vuetifyjs.com/images/logos/vuetify-name-dark.pn"
          width="100"
        />
      </div>

      <v-spacer></v-spacer>

      <v-btn
        
        target="_blank"
        class="text-white"
      >
       
        <span  class="mr-2" v-if="isLoggedIn"><a class="text-white"  @click="logout" >Logout</a></span>
         <span  class="mr-2" v-else><a class="text-white"   >Register</a></span>
        <v-icon>mdi-open-in-new</v-icon>
      </v-btn>
    </v-app-bar>

    <v-main>
      <router-view/>
    </v-main>
  </v-app>
</template>

<style scoped>
text{
  color: white;
  font-weight: 500;
}
</style>

<script>
  export default {
    computed : {
      isLoggedIn : function(){ return this.$store.getters.isLoggedIn}
    },
    methods: {
      logout: function () {
        this.$store.dispatch('logout')
        .then(() => {
          this.$router.push('/about')
        })
      }
    },
  }
</script>
