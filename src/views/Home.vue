<template>
<v-container>	
 <v-row> 
 <v-col cols="6">
 <v-card class="cardCss" dark>
 <v-card-title>User Story - US123445</v-card-title>
 <v-form class="cardCss"
    ref="form"
    v-model="valid"
    lazy-validation
  >
    <v-text-field
      v-model="name"
      :counter="10"
      :rules="nameRules"
      label="Name"
      required
    ></v-text-field>
    <v-text-field
      v-model="number"
      :counter="9"
      :rules="numberRules"
      label="SSO"
      required
    ></v-text-field>
    <number-input ref="price" />
    <v-checkbox
      v-model="checkbox"
      :rules="[v => !!v || 'You must agree to continue!']"
      label="I agree to the Terms and Condition"
      required
    ></v-checkbox>
    <v-btn
      :disabled="!valid"
      color="success"
      class="mr-4"
      @click="submit"
    >
      Submit
    </v-btn>
  </v-form>
</v-card>
</v-col>
<v-col cols="6">
<v-card	class="cardCss" dark>
	<v-card-title>User Details</v-card-title>
 <Details ref="details"/>
</v-card>
</v-col>
</v-row>
</v-container>
</template>
<style>
 .cardCss{
 padding:20px;
 }
</style>	
<script>
import axios from "axios";
import NumberInput from "@/components/NumberInput";
import Details from "@/components/Details";
export default {
components: { NumberInput, Details },
data: () => ({
	valid: true,
	name: '',
	nameRules: [
	v => !!v || 'Name is required',
	v => (v && v.length <= 10) || 'Name must be less than 10 characters',
	],
	number: '',
	numberRules: [
	v => !!v || 'Number is required',
	v => (v && v.length == 9) || 'SSO should be 9 digits',
	v => /^\d+$/.test(v) || 'SSO field takes only number',
	],
	checkbox: false,
}),
methods: {
	submit () {
		if(this.$refs.form.validate()){
		console.log("Data Posted to API")
		let data=this.$refs.price.$data;
		let user={
		name:this.name,
		sso:this.number,
		amount:parseFloat(data.price),
		logo:"img/user.png"
		}
		console.log(user);
		this.postDataAPI(user)
		}
    },
    postDataAPI(user) {
      this.loading = true;
      axios.post("http://localhost:3000/users", user)
        .then((response) => {
          this.loading = false;
          console.log(response)
          this.$refs.details.readDataFromAPI();
        }).catch(error => {
    console.log(error);
    });
    },
 }
};
</script>
