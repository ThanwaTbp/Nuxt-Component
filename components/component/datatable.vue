<template>
	<v-text-field v-model="searchField" label="ค้นหาเหรียญ"></v-text-field>

	<e-data-table
		:headers="headers"
		:items="items"
		:search-field="searchField"
		:search-value="searchValue"
		:rows-items="[5, 10, 25, 50, 100]"
		:server-items-length="serverItemsLength"
		rows-per-page-message="จำนวนหน้าที่เลือก :"
		rows-of-page-separator-message="จาก"
		empty-message="ไม่พบข้อมูล"
		v-model:server-options="serverOptions"
		v-model:items-selected="itemsSelected"
		:loading="loading"

		@click-row="showRow"

		alternating
		show-index
		buttons-pagination

		theme-color="#41c2cc"
		table-class-name="customize-table"
		header-text-direction="center"
		body-text-direction="center"
	>
	<template #item-changePercent24Hr="item">
		<h4 :class="item.changePercent24Hr > 0 ? 'text-success mb-0' : 'text-error mb-0'">
			<b>{{ parseFloat(item.changePercent24Hr).toFixed(2) }}</b>
		</h4>
	</template>
	<template #item-priceUsd="item">
		<b class="text-success">$</b> {{ parseFloat(item.priceUsd).toFixed(2) }}
	</template>
	<template #item-operation="item">
		<div class="d-flex justify-center align-center">
			<v-btn class="mx-1" size="x-small" icon="mdi-pencil" color="primary" />
			<v-btn class="mx-1" size="x-small" icon="mdi-delete" color="error" />
		</div>
	</template>
	</e-data-table>
	<h1>row clicked: <pre id="row-clicked"></pre></h1>

	<!-- syntex อื่นๆที่อาจใช้ -->
	<!-- <pre class="mt-5">
		:current-page=2 //เปิดมาแล้วเลือกหน้าที่ 2
		<hr>
		hide-rows-per-page // ซ่อน Filter หน้า
		<hr>
		hide-footer // ซ่อน Footer
		<hr>
		border-cell // เพิ่มขอบ
		<hr>
		no-hover // ไม่ hover
		<hr>
		:rows-per-page="10" // กำหน้าหน้า
	</pre> -->
	<!--  -->

</template>

<!-- <script lang="ts">
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

		const searchField:any = ref('')
		const searchValue = ref()

		const serverItemsLength = ref(0)
		const serverOptions = ref<ServerOptions>({
			page: 1,
			rowsPerPage: 10,
			sortBy: searchField,
		})

		const loading = ref(false)

		const loadFromApi = async () => {
			loading.value = true

			const { page, rowsPerPage, sortBy, sortType } = serverOptions.value

			let url = `https://komgrip.co.th/coincap/assets?limit=${rowsPerPage}&offset=${(page - 1) * rowsPerPage}`
			if (sortBy == 'undefined') {
				url = url
			} else {
				url = `https://komgrip.co.th/coincap/assets?limit=${rowsPerPage}&offset=${(page - 1) * rowsPerPage}&search=${sortBy}`
			}

			fetch(url)
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
			loading,
			searchField,
			searchValue,
		}
	},
})
</script> -->

<script lang="ts" setup>

import type { Header, Item, ServerOptions, ClickRowArgument } from 'vue3-easy-data-table'
const headers = ref([
	{ text: "ID", value: "id" },
	{ text: "Symbol", value: "symbol" },
	{ text: "Name", value: "name" },
	{ text: "PriceUsd", value: "priceUsd", sortable: true },
	{ text: "ChangePercent24Hr", value: "changePercent24Hr", sortable: true },
	{ text: "Operation", value: "operation", },
])

const showRow = (item: ClickRowArgument) => {
	document.getElementById('row-clicked').innerHTML = JSON.stringify(item.name);
};

const items = ref<Item[]>([])
const itemsSelected: Item[] = ref([]);

const searchField: any = ref('')
const searchValue = ref()

const serverItemsLength = ref(0)
const serverOptions = ref<ServerOptions>({
	page: 1,
	rowsPerPage: 10,
	sortBy: searchField,
})

const loading = ref(false)

const loadFromApi = async () => {
	loading.value = true

	const { page, rowsPerPage, sortBy, sortType } = serverOptions.value

	let url = `https://komgrip.co.th/coincap/assets?limit=${rowsPerPage}&offset=${(page - 1) * rowsPerPage}`
	if (sortBy == 'undefined') {
		url = url
	} else {
		url = `https://komgrip.co.th/coincap/assets?limit=${rowsPerPage}&offset=${(page - 1) * rowsPerPage}&search=${sortBy}`
	}

	fetch(url)
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

</script>

<style>
.customize-table {

	--easy-table-header-font-size: 14px;
	--easy-table-header-height: 50px;
	--easy-table-header-font-color: #fff;
	--easy-table-header-background-color: #41c2cc;

	--easy-table-header-item-padding: 10px 15px;
}
</style>