<template>
	<div class="container">
		<SearchForm @search-users="searchUsers" @clear-users="clearUsers" />
		<Users :users="users" :loading="loading" />
	</div>
</template>

<script>
import axios from 'axios';

import SearchForm from '../components/SearchForm';
import Users from '../components/Users';

export default {
	name: 'Home',
	components: {
		SearchForm,
		Users,
	},
	data() {
		return {
			users: [],
			loading: false,
		};
	},
	methods: {
		searchUsers(term) {
			const fetchData = async () => {
				this.loading = true;
				const res = await axios.get('https://api.github.com/search/users', {
					params: {
						q: term,
						client_id: process.env.VUE_APP_GITHUB_CLIENT_ID,
						client_secret: process.env.VUE_APP_GITHUB_CLIENT_ID,
					},
				});

				this.users = res.data.items;
				this.loading = false;
			};

			fetchData();
		},
		clearUsers() {
			this.users = [];
		},
	},
};
</script>
