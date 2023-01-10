<script setup lang="ts">

definePageMeta({
	layout: "backend",
})

useHead({
	title: 'Product',
	meta: [
		{
			name: 'keywords',
			content: 'Product, Nuxt 3, Backend'
		},
		{
			name: 'Description',
			content: 'Product Nuxt 3,  IT Genius Engineering'
		}
	]
})

const { $swal } = useNuxtApp()

const success = () => {
	$swal.fire({
		title: 'Success!',
		text: 'Do you want to continue',
		icon: 'success',
		confirmButtonText: 'So Cool !!'
	})
};

const error = () => {
	$swal.fire({
		title: 'Error!',
		text: 'Do you want to continue',
		icon: 'error',
		confirmButtonText: 'So Cool !!'
	})
};

const question = () => {
	$swal.fire({
		title: 'Question!',
		text: 'Do you want to continue',
		icon: 'question',
		confirmButtonText: 'So Cool !!'
	})
};

const warning = () => {
	$swal.fire({
		title: 'Warning!',
		text: 'Do you want to continue',
		icon: 'warning',
		confirmButtonText: 'So Cool !!'
	})
};

const info = () => {
	$swal.fire({
		title: 'Info!',
		text: 'Do you want to continue',
		icon: 'info',
		confirmButtonText: 'So Cool !!'
	})
};


</script>

<template>
	<div>
		<h1 class="mb-5">Sweetalert2</h1>

		<v-container>
			<v-row>
				<v-col lg="2">
					<v-btn color="success" @click="success">
						Success
						<v-tooltip activator="parent" location="bottom">
							Tooltip
						</v-tooltip>
					</v-btn>
				</v-col>
				<v-col lg="2">
					<v-btn color="error" @click="error">
						Error
						<v-tooltip activator="parent" location="bottom">
							Tooltip
						</v-tooltip>
					</v-btn>
				</v-col>
				<v-col lg="2">
					<v-btn color="primary" @click="question">
						Question
						<v-tooltip activator="parent" location="bottom">
							Tooltip
						</v-tooltip>
					</v-btn>
				</v-col>
				<v-col lg="2">
					<v-btn color="warning" @click="warning">
						Warning
						<v-tooltip activator="parent" location="bottom">
							Tooltip
						</v-tooltip>
					</v-btn>
				</v-col>
				<v-col lg="2">
					<v-btn color="info" @click="info">
						Info
						<v-tooltip activator="parent" location="bottom">
							Tooltip
						</v-tooltip>
					</v-btn>
				</v-col>
			</v-row>
		</v-container>
	</div>
</template>

<style scoped>

</style>
