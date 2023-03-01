<template>
    <label :for="name"></label>
    <select :name="name">
            <option 
                v-for="(option, index) in options"
                :value="option"
                :key="index"
                @click="$emit('setSelection', option)"
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
    emits: ['setSelection']
}
</script>

<style>

</style>