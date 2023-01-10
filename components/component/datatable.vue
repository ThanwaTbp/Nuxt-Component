<template>
	<v-text-field v-model="searchValue" label="ค้นหาเหรียญ"></v-text-field>

	<e-data-table
	:headers="headers"
	:items="cryp"
	:search-field="searchField"
	:search-value="searchValue"
	rows-per-page-message="จากทั้งหมด 100 หน้า"
	rows-of-page-separator-message="จาก"
	empty-message="ไม่พบข้อมูล"
	:rows-per-page="10"

	alternating
	show-index
	buttons-pagination

	theme-color="#2d3a4f"
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
	</e-data-table>
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
	</pre> -->
	<!--  -->

</template>

<script lang="ts" setup>
const res = await fetch(`https://api.coincap.io/v2/assets`)
const item = await res.json()
const cryp = item.data

const searchField = ref(["name", "symbol"])
const searchValue = ref("");

const headers = ref([
	{ text: "ID", value: "id" },
	{ text: "Symbol", value: "symbol" },
	{ text: "Name", value: "name" },
	{ text: "PriceUsd", value: "priceUsd", sortable: true },
	{ text: "ChangePercent24Hr", value: "changePercent24Hr", sortable: true },
	// { text: "Edit", value: null, sortable: true },
])


</script>

<style>
.customize-table {

	--easy-table-header-font-size: 14px;
	--easy-table-header-height: 50px;
	--easy-table-header-font-color: #c1cad4;
	--easy-table-header-background-color: #2d3a4f;

	--easy-table-header-item-padding: 10px 15px;
}
</style>