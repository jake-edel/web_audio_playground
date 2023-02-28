<template>
    <label :for="name"></label>
    <select :name="name">
        <!-- @change="setSelection(value)" -->
            <option 
                v-for="(option, index) in options"
                :value="option"
                :key="index"
                @click="setSelection(option)"
            >
                {{ option[0].toUpperCase() + option.substring(1) }}
            </option>
    </select>
</template>

<script>
export default {
    props: {
        name: {
            type: String,
            required: true
        },
        options: {
            type: Array,
            required: true
        }
    },
    methods: {
        setSelection(selection) {
            console.log('event emitted, settingSelecton to ', selection)
            this.$emit('setSelection', selection)
        }
    }

}
</script>

<style>

</style>