<template>
	<div>
		<!-- <DataTable
            buttons-pagination
            :headers="headers"
            :items="items"
            :rows-items="[5, 10, 25, 50, 100]"
            :rows-per-page="5"
            :show-index="true"
            table-class-name="customize-vue3-easy-data-table"
            header-text-direction="center"
            body-text-direction="center"
        /> -->

		<e-data-table v-model:server-options="serverOptions" :headers="headers" :items="items"
			:rows-items="[5, 10, 25, 50, 100]" table-class-name="customize-vue3-easy-data-table"
			:server-items-length="serverItemsLength" :loading="loading" buttons-pagination />

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
			{ text: "Symbol", value: "symbol" },
			{ text: "Name", value: "name" },
			{ text: "PriceUsd", value: "priceUsd", sortable: true },
			{ text: "ChangePercent24Hr", value: "changePercent24Hr", sortable: true },
		]
		const items = ref<Item[]>([])

		const serverItemsLength = ref(0)
		const serverOptions = ref<ServerOptions>({
			page: 1,
			rowsPerPage: 5,
		})

		const restApiUrl = computed(() => {
			const { page, rowsPerPage, sortBy, sortType } = serverOptions.value
			return `https://komgrip.co.th/coincap/assets?limit=${rowsPerPage}&offset=${(page - 1) * rowsPerPage
				}`
		})

		const loading = ref(false)

		const loadFromApi = async () => {
			loading.value = true

			const { page, rowsPerPage, sortBy, sortType } = serverOptions.value
			fetch(
				`https://komgrip.co.th/coincap/assets?limit=${rowsPerPage}&offset=${(page - 1) * rowsPerPage
				}`
			)
				.then((response) => response.json())
				.then((data) => {
					let cryptocurrencies = data
					items.value = cryptocurrencies.data
					serverItemsLength.value = 100
					loading.value = false
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

