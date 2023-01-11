<script lang="ts" setup>
definePageMeta({
	layout: "backend",
})

useHead({
	title: 'Report',
	meta: [
		{
			name: 'keywords',
			content: 'Report, Nuxt 3, Backend'
		},
		{
			name: 'Description',
			content: 'Report Nuxt 3'
		}
	]
})
</script>

<template>
	<ComponentDatatable />
	<br><br>
	<!-- <ComponentDatatable2 />
	<br><br>
	<ComponentDatatable3 /> -->
</template>

<style>

</style>