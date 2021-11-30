<template>
    <div>
        <input v-model="Text" type="text">
        <button @click="$emit('searchText', Text)">Click Me</button>
    </div>
</template>

<script>
export default {
    name: 'Form',
    data() {
        return {
            Text: '',
        }
    }
}
</script>

<style>

</style>