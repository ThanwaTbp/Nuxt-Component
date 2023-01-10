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
				content: 'Multiselect | Nuxt 3'
			}
		]
	})

// const { data: cryptoAssets } = useFetch<any>('https://api.coincap.io/v2/assets');
// const crypto = computed(() => cryptoAssets.value)
// const currentAsset = ref(null)
// const { data: crypto } = await useFetch(`https://api.coincap.io/v2/assets`, { pick: ['data', 'timestamp'] })

const res = await fetch(`https://api.coincap.io/v2/assets`)
const item = await res.json()
const cryp = item.data

const values:any = []

</script>

<template>
	<div>
		<v-container>
			<Multiselect v-model="values" :searchable="true" :multiple="true" :options="cryp" value-prop="name" mode="tags" track-by="name" label="name" placeholder="Select Item" :close-on-select="false" />
			<br>
			<pre><code>{{ values }}</code></pre>
		</v-container>
	</div>
</template>


<style src="@vueform/multiselect/themes/default.css">

</style>