<template>
	<div>
		<Loading v-if="loading" />
		<div v-else class="user-style">
			<UserItem :key="user.id" v-for="user in users" :user="user" />
		</div>
	</div>
</template>

<script>
import UserItem from './UserItem';
import Loading from './layout/Loading';

export default {
	name: 'Users',
	components: {
		UserItem,
		Loading,
	},
	props: {
		users: {
			type: Array,
			required: true,
		},
		loading: {
			type: Boolean,
			required: true,
		},
	},
};
</script>

<style scoped>
.user-style {
	display: grid;
	grid-template-columns: repeat(3, 1fr);
	grid-gap: 1rem;
}
</style>
