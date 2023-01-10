<script setup lang="ts">

definePageMeta({
	layout: "backend",
})

useHead({
	title: 'Order',
	meta: [
		{
			name: 'keywords',
			content: 'Order, Nuxt 3, Backend'
		},
		{
			name: 'Description',
			content: 'Order Nuxt 3,  IT Genius Engineering'
		}
	]
})

const value:any = []
const options = [
	{ name: 'Vue.js', language: 'JavaScript' },
	{ name: 'Adonis', language: 'JavaScript' },
	{ name: 'Rails', language: 'Ruby' },
	{ name: 'Sinatra', language: 'Ruby' },
	{ name: 'Laravel', language: 'PHP' },
	{ name: 'Phoenix', language: 'Elixir' }
]
</script>

<template>
	<div>
		<label class="typo__label">Simple select / dropdown</label>
		<multiselect v-model="value" :options="options" mode="tags" value-prop="name" :multiple="true" :close-on-select="false" :clear-on-select="false"
			:preserve-search="true" placeholder="Pick some" label="name" track-by="name" :preselect-first="true">
			<template slot="selection" slot-scope="{ values, search, isOpen }"><span class="multiselect__single"
					v-if="values.length &amp;&amp; !isOpen">{{ values.length }} options selected</span></template>
		</multiselect>
		<pre class="language-json"><code>{{ value  }}</code></pre>
	</div>
</template>

<style scoped>

</style>