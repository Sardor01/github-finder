<template>
	<div class="card">
		<h3>
			<a :href="repo.html_url">{{ repo.name }}</a>
		</h3>
		<p>{{ repo.description }}</p>
	</div>
</template>

<script>
export default {
	name: 'RepoItem',
	props: {
		repo: {
			type: Object,
			required: true,
		},
	},
};
</script>

<style></style>
