<template>
	<div class="container">
		<div class="controls">
			<!-- <button class="ctrl-btn" @click="createAudioContext">
				Create Audio Context
			</button> -->
			<button class="ctrl-btn" @click="startOscillator">
				Start Oscillator
			</button>
			<button class="ctrl-btn" @click="stopOscillator">
				Suspend Oscillator
			</button>
			<button class="ctrl-btn" @click="resumeOscillator">
				Resume Oscillator
			</button>
			<DropdownSelect :name="'waveforms'" :options="waveforms" @setSelection="setWaveform(waveform)"/>
			<input type="range" min="40" max="15000" v-model="oscFrequency">
			<div>
				Current Frequency: {{ oscFrequency }}
			</div>
		</div>
	</div>
</template>

<script>
import DropdownSelect from '../controls/DropdownSelect.vue'

export default {
	components: {
		DropdownSelect
	},
	data () {
		return {
			oscillator: null,
			oscFrequency: 600,
			waveform: 'sine',
			waveforms: ['sine', 'square', 'sawtooth', 'triangle']
		}
	},
	props: {
		audioContext: {
			type: Object,
			required: true
		}
	},
	computed: {

	},
	methods: {
		startOscillator () {
			this.oscillator = this.audioContext.createOscillator()
			this.oscillator.connect(this.audioContext.destination)
			this.oscillator.start()
		},
		stopOscillator () {
			this.audioContext.suspend().then(() => { console.log('Audio Context Suspended') })
		},
		resumeOscillator () {
			this.audioContext.resume().then(() => { console.log('Audio Context Resumed') })
		},
		setWaveform (newWaveform) {
			console.log('arg emitted: ', newWaveform)
			console.log('setting waveform from ', this.waveform, ' to ', newWaveform)
			this.waveform = newWaveform
		}
	},
	watch: {
		oscFrequency () {
			this.oscillator.frequency.value = this.oscFrequency
		},
		waveform () {
			console.log('waveform changed', this.waveform)
			this.oscillator.type = this.waveform
		}

	}
}
</script>

<style lang="scss">
	.container {
		background-color: $btn-green;
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