<template>
	<div class="card text-center">
		<img
			:src="user.avatar_url"
			alt="User Image"
			class="round-img"
			style="width: 60px"
		/>

		<h4>{{ user.login }}</h4>

		<div>
			<router-link
				v-bind:to="`/users/${user.login}`"
				class="btn btn-dark btn-sm my-1"
			>
				More
			</router-link>
		</div>
	</div>
</template>

<script>
export default {
	name: 'UserItem',
	props: {
		user: {
			type: Object,
			required: true,
		},
	},
};
</script>

<style></style>
