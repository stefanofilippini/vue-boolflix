<template>
    <div>
        <input v-model="Text" @keyup.enter="$emit('searchText', Text)" type="text">
        <button @click="$emit('searchText', Text)">Search</button>
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