<template>
	<div :ref="containerClassRef" :class="containerClassRef">...loading</div>
</template>

<script>
const longdoMapApiKey = "7fc3a83b6bc03d721478d921ad8b1857";

export default {
	data() {
		return {
			longdo: null,
			map: null,
			containerClassRef: "longdo-map-container",
			scriptTagId: "longdo-map-script",
		};
	},
	mounted() {
		this.addScript();
	},
	methods: {
		addScript() {
			const self = this;
			const existingScript = document.getElementById(self.scriptTagId);

			if (!existingScript && !self.longdo) {
				const script = document.createElement("script");
				script.src = `https://api.longdo.com/map/?key=${longdoMapApiKey}`;
				script.id = self.scriptTagId;
				document.body.appendChild(script);

				script.onload = () => {
					self.longdo = window.longdo;

					self.initialMap();
				};
			} else {
				self.initialMap();
			}
		},
		initialMap() {
			const self = this;
			self.map = new self.longdo.Map({
				placeholder: self.$refs[self.containerClassRef],
			});
			self.map.Event.bind("ready", () => {
				self.$emit("loaded", self.longdo, self.map);
			});
		},
	},
};
</script>

<style scoped>
.longdo-map-container {
	width: 100%;
	height: 100%;
}
</style>
