<template>
	<div class="map-wraper">
		<LongdoMap @loaded="onLoadedLongdoMap" />
	</div>
</template>

<script lang="ts">
export default {
	data() {
		return {
			longdo: null,
			map: null,
		};
	},
	methods: {
		onLoadedLongdoMap(longdo, map) {
			this.longdo = longdo;
			this.map = map;

			this.map.Overlays.add(
				new this.longdo.Marker({
					lat: 13,
					lon: 100,
				})
			);
			this.map.zoom(12);

			console.log(this.longdo, this.map);
		},
	},
};
</script>

<style>
.map-wraper {
	width: 500px;
	height: 500px;
}
</style>
