<template>
	<div v-if="alertMessage !== ''" class="alert alert-light d-flex">
		<div>
			<i class="fas fa-info-circle m"></i> <span>{{ alertMessage }}</span>
		</div>
		<i class="fas fa-minus-circle delete" @click="$emit('remove-alert')"></i>
	</div>
</template>

<script>
export default {
	name: 'Alert',
	props: {
		alertMessage: {
			type: String,
			required: true,
		},
	},
};
</script>

<style></style>
