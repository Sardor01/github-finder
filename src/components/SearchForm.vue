<template>
	<div>
		<Alert :alertMessage="alertMessage" @remove-alert="removeAlert" />
		<form class="form-text" @submit.prevent="handleSubmit">
			<input
				type="text"
				name="term"
				v-model="searchTerm"
				placeholder="Seach Users..."
			/>
			<input type="submit" value="Search" class="btn btn-dark btn-block" />
		</form>
		<button class="btn btn-light btn-block" @click="$emit('clear-users')">
			Clear
		</button>
	</div>
</template>

<script>
import Alert from './layout/Alert';

export default {
	name: 'SearchForm',
	components: {
		Alert,
	},
	data() {
		return {
			searchTerm: '',
			alertMessage: '',
		};
	},
	methods: {
		handleSubmit() {
			if (this.searchTerm !== '') {
				this.$emit('search-users', this.searchTerm);
			} else {
				this.alertMessage = 'Please enter something';

				setTimeout(() => {
					this.alertMessage = '';
				}, 5000);
			}
			// Clear input
			this.searchTerm = '';
		},
		removeAlert() {
			this.alertMessage = '';
		},
	},
};
</script>

<style></style>
