<template>
  <v-container>
   <h1 clas="display-4">Welcome to alongkab</h1>
   <h4>Total Wallet Balance: {{wallet}}</h4>




  

      <v-btn
      color="warning"
      elevation="2"
    >
      <paystack
        :amount="amount"
        :email="email"
        :paystackkey="paystackkey"
        :reference="reference"
        :callback="callback"
        :close="close"
        :embed="false"
    >
       <i class="fas fa-money-bill-alt"></i>
       Add Funds
    </paystack>
    </v-btn>

    


  


  </v-container>
</template>

<script>
import paystack from 'vue-paystack';
import axios from 'axios';
export default {
  name: 'HelloWorld',
    components: {
        paystack
    },
     data: function(){
        return{
          wallet: '',
          paystackkey: "pk_test_c87df395813436d6b32044a71dd220dc78c9b222", //paystack public key
          email: "user@alongkab.com", // Customer email
          amount: 1000000, // in kobo
          
          bal: '',
        }
    },
    mounted() {

         this.getbalance();

        
    },
   
    computed: {
      reference(){
        let text = "";
        let possible = "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789";

        for( let i=0; i < 10; i++ )
          text += possible.charAt(Math.floor(Math.random() * possible.length));

        return text;
      }
    },
    methods: {

      getbalance(){
var vm = this;
            let user_id = localStorage.getItem('user_id')

         axios.post('http://localhost:3000/api/user_wallet', {
          user_id: user_id,
         
        })
        .then(function (response) {

        vm.wallet = response.data.total
         
          console.log(response.data.total);
        })
        .catch(function (error) {
          console.log(error);
        })
      },
      callback: function(response){

          const user_id = localStorage.getItem('user_id')


        axios.post('http://localhost:3000/api/fund_wallet', {
          user_id: user_id,
          amount: this.amount,
          type: 'credit',
          description: 'Wallet Funds added'
        })
        .then(function (response) {

          console.log(response);
        })
        .catch(function (error) {
          console.log(error);
        });

        // console.log(response)

      },


      close: function(){
          console.log("Payment closed")
      }
    }
}
</script>
