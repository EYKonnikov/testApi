<script setup>
	import {
		ref,
		onMounted,
		onUnmounted
	} from 'vue'


	let watcher;
	const gpsTime = ref(Date.now());
	const coordinates = ref({
		accuracy: 0,
		latitude: 0,
		longtitude: 0,
		altitude: 0,
		altitudeAccuracy: 0,
		heading: 0,
		speed: 0
	});


	function setPosition(payload) {
		gpsTime.value = payload.timestamp
		coordinates.value = payload.coords
		console.log(coordinates.value)
	}

	onMounted(() => {
		if (Geolocation) {
			watcher = navigator.geolocation.watchPosition(setPosition)
		}
	})

	onUnmounted(() => {
		if (watcher) {
			Geolocation.clearWatch(watcher)
		}
	})
</script>

<template>
	<div class="gps">
		<h2 class="gps__title">GPS Position</h2>
		<div class="coordinates">
			<p>latitude: {{coordinates.latitude}}</p>
			<p>longtitude: {{coordinates.longitude}}</p>
		</div>
	</div>


</template>

<style scoped>
	.gps,
	.coordinates {
		display: flex;
		flex-direction: column;
	}

	.gps {
		box-shadow: rgba(50, 50, 93, 0.25) 0px 2px 5px -1px, rgba(0, 0, 0, 0.3) 0px 1px 3px -1px;
		padding: 20px;
	}
	
	.gps__title {
		padding: 10px 0px;
		
	}
	
	
</style>
