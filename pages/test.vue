<script lang="ts" setup>
useHead({
	title: 'บล็อก',
	meta: [
		{
			name: 'keywords',
			content: 'บล็อก, Nuxt 3, Backend'
		},
		{
			name: 'Description',
			content: 'บล็อก Nuxt 3,  THW'
		}
	]
})
const page = ref(1);
// const { data: url } = await useFetch(`https://api.coincap.io/v2/assets`, { pick: ['data','timestamp'], })

const config = useRuntimeConfig()
const { data: cryp } = await useFetch(() => `?limit=${page.value}&offset=${page.value}`, { baseURL: config.API_BASE_URL }

// console.log(cryp)

</script>

<template>
	<div class="mb-5">

		<div class="wrapper">
			<v-row justify="center">
				<v-col cols="12" sm="10" md="9" lg="7">
					<div class="text-center">
						<h2 class="ui-title font-weight-bold text-white mb-4">บล็อกล่าสุด</h2>
						<p class="text-white">
							You can relay on our amazing features list and also our customer services will be great
							experience for you without doubt and in no-time
						</p>
					</div>
				</v-col>
			</v-row>
		</div>
		<v-container>
			<v-row class="mt-13" justify="center">
				<v-col cols="12" md="6" lg="4" v-for="items in cryp.data" :key="items">
					<v-col cols="12" md="6" lg="4">
						<v-card elevation="0" class="blog-card overflow-hidden mb-5">
							<div class="pa-5">
								<div class="d-flex justify-space-between">
									<a href="#" class="blog-title text-decoration-none font-weight-medium font-18">
										{{ items.symbol }}
									</a>
									<v-img lazy-src="https://picsum.photos/id/11/10/6" max-height="70" max-width="120"
										src="https://www.rd.com/wp-content/uploads/2022/08/bitcoin-cryptocurrency-GettyImages-1336750482.jpg?fit=700,1024">
									</v-img>
								</div>
								<p class="mt-10 mb-10">
									{{ parseFloat(items.supply).toFixed(2) }} / {{
										parseFloat(items.maxSupply).toFixed(2)
									}}
								</p>
								<h2>${{ parseFloat(items.priceUsd).toFixed(2) }}</h2>
								<h1 :class="items.changePercent24Hr <= 0 ? 'text-red' : 'text-success'">{{
									parseFloat(items.changePercent24Hr).toFixed(2)
								}}</h1>
							</div>
						</v-card>
					</v-col>
				</v-col>
			</v-row>
		</v-container>

	</div>
</template>

<style scoped>
.ui-title {
	font-size: 32px;
}

.font-18 {
	font-size: 18px;
}

.wrapper {
	background: #2196F3;
	padding: 40px 0 20px;
	min-height: 400px;
	display: flex;
	align-items: center;
	margin-bottom: 20px;
}

.blog-card {
	transition: 0.2s ease-in;
}

.blog-card:hover {
	transform: translateY(-10px);
}

.blog-title {
	color: #263238 !important;
	line-height: 22px;
	font-weight: bold;
}

.blog-title:hover {
	color: #607df9 !important;
}
</style>