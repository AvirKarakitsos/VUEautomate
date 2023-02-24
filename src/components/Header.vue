<template>
	<nav>
		<img src="../assets/logo.png" alt="">
		<p>Vue JS</p>
	</nav>
  
</template>

<script>
export default {
  name: 'Header'
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
	nav{
		height: 4rem;
		display: flex;
		align-items: center;
		border-bottom: 1px solid rgb(243 244 246);
		background-color: white;
	}
	img{
		width: 3rem;
		height: 3rem;
		position: relative;
		left: 175px;
	}
	p{
		position: relative;
		left: 190px;
		font-size: 1rem;
		font-weight: 600;
		color: rgb(31 41 55);
	}
</style>
