<script setup>
import OscillatorSimple from '../components/OscillatorSimple.vue'
</script>

<template>
	<main>
		<button @click="createAudioContext">Create Audio Context</button>
		<div v-if="audioContextCreated">
			<OscillatorSimple :audioContext="audioContext"/>
		</div>
	</main>
</template>

<script>
	export default {
		data () {
			return {
				audioContext: null,
				audioContextCreated: false
			}
		},
		methods: {
			createAudioContext () {
				this.audioContext = new AudioContext()
				this.audioContextCreated = true
			}
		}
	}
</script>
