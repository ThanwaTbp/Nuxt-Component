<template>
	<div>
		<e-data-table v-model:server-options="serverOptions" :headers="headers" :items="items"
			:rows-items="[5, 10, 25, 50, 100]" table-class-name="customize-vue3-easy-data-table"
			:server-items-length="serverItemsLength" :loading="loading" buttons-pagination show-index >
			<template #item-image_url="item">
				<img :src="item.image_url" alt="" width="20">
			</template>
		</e-data-table>
		{{ restApiUrl }}
	</div>
</template>

<script lang="ts">
import { defineComponent, ref, computed, watch } from 'vue'
import type { Header, Item, ServerOptions } from 'vue3-easy-data-table'

export default defineComponent({
	setup() {
		const headers: Header[] = [
			{ text: "ID", value: "id" },
			{ text: "IMG", value: "image_url" },
			{ text: "Name", value: "name" },
			{ text: "Description", value: "description"},
		]
		const items = ref<Item[]>([])

		const serverItemsLength = ref(0)
		const serverOptions = ref<ServerOptions>({
			page: 1,
			rowsPerPage: 5,
		})

		const restApiUrl = computed(() => {
			const { page, rowsPerPage, sortBy, sortType } = serverOptions.value
			return `https://api.punkapi.com/v2/beers?page=${page}&per_page=${rowsPerPage}`
		})

		const loading = ref(false)

		const loadFromApi = async () => {
			loading.value = true

			const { page, rowsPerPage, sortBy, sortType } = serverOptions.value
			fetch(
				// `https://api.coincap.io/v2/assets?limit=${rowsPerPage}&offset=${(page - 1) * rowsPerPage}`
				`https://api.punkapi.com/v2/beers?page=${page}&per_page=${rowsPerPage}`
			)
				.then((response) => response.json())
				.then((data) => {
					let beer = data
					items.value = beer
					serverItemsLength.value = 100
					loading.value = false
					console.log(data)
				})
		}

		loadFromApi()

		watch(
			serverOptions,
			(value) => {
				loadFromApi()
			},
			{ deep: true }
		)

		return {
			headers,
			items,
			serverOptions,
			serverItemsLength,
			restApiUrl,
			loading,
		}
	},
})
</script>

<style scoped>

</style>

