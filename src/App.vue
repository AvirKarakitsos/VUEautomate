<template>

	<body>
		<Header/>
		<Formulaire/>
	</body>
	
</template>

<script>
	import Header from "./components/Header.vue"
	import Formulaire from "./components/Formulaire.vue"
	export default {
	name: 'App',
	components: {
		Header,
		Formulaire,
	},
}
</script>

<style>
	*{
		margin: 0;
		padding: 0;
		box-sizing: border-box;
	}
	body{
		font-size: 1.1rem;
		font-weight: bold;
		text-align: center;
	}
</style>

