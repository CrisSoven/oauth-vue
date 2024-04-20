<template>
	<div class="container">
		<GoogleLogin :callback="callback" prompt auto-login />
		<br /><br /><br />
		<div v-if="loggedIn">
			<h2>Bienvenido {{ user.name }}</h2>
			<h2>{{ user.email }}</h2>
			<br />
			<img class="image" :src="user.picture" />
			<button class="btn" @click="logout">logout</button>
		</div>
	</div>
</template>

<script setup>
import { ref } from 'vue';
import { GoogleLogin, decodeCredential, googleLogout } from 'vue3-google-login';

const loggedIn = ref(false);
const user = ref(null);

const callback = (response) => {
	loggedIn.value = true;
	user.value = decodeCredential(response.credential);
};

const logout = () => {
	googleLogout();
	loggedIn.value = false;
	user.value = null;
};
</script>

<style>
.container {
	width: 50rem;
	margin: 0 auto;
	text-align: center;
	padding: 20px;
	border: 1px solid #ccc;
	border-radius: 5px;
	background-color: #f8f8f8;
}

.btn {
	width: 100%;
	padding: 10px;
	border: 1px solid #ccc;
	border-radius: 5px;
	background-color: #f1f1f1;
	color: #42b983;
	font-size: 18px;
	font-weight: bold;
	text-transform: uppercase;
	margin-top: 2rem;
}

.image {
	width: 200px;
	height: 200px;
	border-radius: 50%;
}

h2 {
	margin: 0;
	padding: 0;
	font-size: 18px;
	font-weight: bold;
	color: #42b983;
}
</style>
