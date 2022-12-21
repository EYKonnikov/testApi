<script setup>
	const {
		createApp,
		defineComponent,
		setup,
		ref,
		onMounted,
		onUnmounted
	} = Vue
	
	
	const fetchLocation = () => {
		let watcher;
		const geoLocation = navigator.geolocation;
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
		
		const setPosition = (payload) => {
			gpsTime.value = payload.timestamp
			coordinates.value = payload.coords
		}
		
		
	}
	
	onMounted(() => {
		if(geoLocation) {
			watcher = geoLocation.watchPosition(setPosition);
		}
	})
	
	   
	
</script>

<template>
	<h2>GPS Position</h2>
</template>

<style scoped>

</style>
