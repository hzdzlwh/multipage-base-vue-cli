<template>
	<div class="login" id="login">
		<h1>login</h1>
    <v-button @click.native="loginAction" text="aa"></v-button>
    <a href="welcome.html">welcome</a>
	</div>
</template>

<script>
import {Lib} from 'assets/Lib.js';
import VButton from 'components/Button';

console.log(Lib)
export default {
	data() {
		return {

		}
	},
	components: {
		VButton
	},
  methods: {
    loginAction: function(){
        window.location.href = "welcome.html";

    }
  }
}


</script>

<style scoped>
.login{
  text-align: center;
}
</style>





