<template>
	<div>
		<RepoItem :key="repo.id" v-for="repo in repos" :repo="repo" />
	</div>
</template>

<script>
import RepoItem from './RepoItem';

export default {
	name: 'UserRepos',
	components: {
		RepoItem,
	},
	props: {
		repos: {
			type: Array,
			required: true,
		},
	},
};
</script>

<style></style>
