<template>
	<header class="bg-primary">
		<nav class="navbar container">
			<router-link to="/">
				<h1><i class="fab fa-github"></i> Github Finder</h1>
			</router-link>

			<ul>
				<li><router-link to="/">Home</router-link></li>
				<li><router-link to="/about">About</router-link></li>
			</ul>
		</nav>
	</header>
</template>

<script>
export default {
	name: 'Header',
};
</script>

<style></style>
