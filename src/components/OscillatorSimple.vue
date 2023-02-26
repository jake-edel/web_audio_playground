<template>
	<div class="container">
		<div class="controls">
			<button class="ctrl-btn" @click="createAudioContext">
				Create Audio Context
			</button>
			<button class="ctrl-btn" @click="startOscillator">
				Start Oscillator
			</button>
			<button class="ctrl-btn" @click="stopOscillator">
				Suspend Oscillator
			</button>
			<button class="ctrl-btn" @click="resumeOscillator">
				Resume Oscillator
			</button>
			<input type="range" min="40" max="15000" v-model="oscFrequency">
			<div>
				Current Frequency: {{ oscFrequency }}
			</div>
		</div>
	</div>
</template>

<script>
export default {
	data () {
		return {
			audioContext: null,
			oscillator: null,
			oscFrequency: 600
		}
	},
	computed: {
		newTest () {
			return 'test' + ' new'
		}
	},
	methods: {
		createAudioContext () {
			this.audioContext = new AudioContext
			this.oscillator = this.audioContext.createOscillator()
			this.oscillator.connect(this.audioContext.destination)
			console.log('Audio Context Created: ', this.audioContext)
			console.log('Oscillator Created: ', this.oscillator)
		},
		startOscillator () {
			this.oscillator.start()
		},
		stopOscillator () {
			this.audioContext.suspend().then(() => { console.log('Audio Context Suspended') })
		},
		resumeOscillator () {
			this.audioContext.resume().then(() => { console.log('Audio Context Resumed') })
		}
	},
	watch: {
		oscFrequency () {
			this.oscillator.frequency.value = this.oscFrequency
		}
	}
}
</script>

<style lang="scss">
	.container {
		background-color: hsla(160, 100%, 37%, 1);
		border-radius: 10px;
		padding: 10px;
		margin: 10px;
		.controls {
			padding: 0px;
			text-align: center;
			display: flex;
			flex-direction: column;
			.ctrl-btn {
				width: 100px
			}
		}
	}
</style>