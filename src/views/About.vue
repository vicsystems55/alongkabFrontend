<template>
  <div class="col-md-4 mx-auto mt-5">
    <v-card
      elevation="2"
      class="spacing-playground pa-6"
    fluid
    >

          <h1>Login</h1>
          <v-text-field
            label="Enter Email"
            :rules="rules"
            hide-details="auto"
            v-model="email"
          ></v-text-field>
          <v-text-field 
            type="password"
            label="Enter Password"
            v-model="password"
          ></v-text-field>
          <v-btn
            color="primary"
            depressed
            elevation="2"
            large
            :loading='this.loadx'
            v-on:click="login()"
            
          >LOGIN</v-btn>

    </v-card>
  </div>
</template>
<script>
import axios from 'axios'
  export default {
  created () {


  },
  methods: {

     login() {



      console.log(this.email)

        axios
        .post('http://localhost:1000/api/login', {
          email: this.email,
          password: this.password
        })
        .then(response => {
          console.log(response);
          this.$router.push('/') 
        })
        .catch(error => {
          console.log(error)
          this.errored = true
        })
        .finally(() => this.loading = false)
      
    }

  },
    data: () => ({

      email: '',
      password: '',
      loadx: false,


      
      rules: [
        value => !!value || 'Required.',
        value => (value && value.length >= 3) || 'Min 3 characters',
      ],
    }),
  }
</script>