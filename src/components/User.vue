<template>
	<div>
		<Loading v-if="loading" />
		<div v-else class="container">
			<router-link to="/" class="btn btn-light">
				Back to Search
			</router-link>
			<span>
				<i v-if="user.hireable" class="fas fa-check text-success"></i>
				<i v-else class="fas fa-times-circle text-danger"></i>
			</span>

			<div class="card grid-2">
				<div class="all-center">
					<img
						:src="user.avatar_url"
						alt="Avatar"
						class="round-img"
						style="width: 150px"
					/>
					<h1>{{ user.name }}</h1>
					<p>Location: {{ user.location }}</p>
				</div>

				<div>
					<div v-if="user.bio">
						<h3>BIO</h3>
						<p>{{ user.bio }}</p>
					</div>

					<a :href="user.html_url" class="btn btn-dark my-1">
						Visit Github Profile
					</a>

					<ul>
						<li>
							<strong v-if="user.login">Username: </strong> {{ user.login }}
						</li>
						<li>
							<strong v-if="user.company">Company: </strong> {{ user.company }}
						</li>
						<li><strong v-if="user.blog">Website: </strong> {{ user.blog }}</li>
					</ul>
				</div>
			</div>
			<div class="card text-center">
				<div class="badge badge-primary">Followers: {{ user.followers }}</div>
				<div class="badge badge-success">Following: {{ user.following }}</div>
				<div class="badge badge-light">
					Public Repos: {{ user.public_repos }}
				</div>
				<div class="badge badge-dark">
					Public Gists: {{ user.public_gists }}
				</div>
			</div>
			<UserRepos :repos="repos" />
		</div>
	</div>
</template>

<script>
import axios from 'axios';

import Loading from '../components/layout/Loading';
import UserRepos from './UserRepos';

export default {
	name: 'User',
	components: {
		Loading,
		UserRepos,
	},
	data() {
		return {
			login: this.$route.params.login,
			loading: false,
			user: {},
			repos: [],
		};
	},
	created() {
		const showData = async () => {
			this.loading = true;
			const res = await axios.get(
				`https://api.github.com/users/${this.login}`,
				{
					params: {
						client_id: process.env.VUE_APP_GITHUB_CLIENT_ID,
						client_secret: process.env.VUE_APP_GITHUB_CLIENT_ID,
					},
				},
			);
			this.user = res.data;
		};

		const fetchRepos = async () => {
			const res = await axios.get(
				`https://api.github.com/users/${this.login}/repos`,
				{
					params: {
						per_page: 5,
						sort: 'created',
						direction: 'desc',
						client_id: process.env.VUE_APP_GITHUB_CLIENT_ID,
						client_secret: process.env.VUE_APP_GITHUB_CLIENT_ID,
					},
				},
			);

			this.repos = res.data;
			this.loading = false;
		};

		showData();
		fetchRepos();
	},
};
</script>

<style></style>
