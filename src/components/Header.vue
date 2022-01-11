<template>
    <header>
        <label for="genre">Genere</label>
        <select v-model="selectedGenre" id="genre" @change="$emit('selectChanged', selectedGenre)">
            <option value="">Tutti i generi</option>
            <option v-for="(genre, index) in genres" :key="index" :value="genre">{{ genre }}</option>
        </select>
    </header>
</template>

<script>
export default {
    name: "Header",
    props: {
        genres: Array
    },
    data: function() {
        return {
            selectedGenre: ''
        };
    }
}
</script>

<style scoped lang="scss">
@import '../src/styles/variables.scss';
header {
    background-color: $primary_color;
    color: white;
    padding: 20px;
    height: 70px;
    select {
        min-width: 250px;
        margin: 0 20px;
        padding: 5px;
        font-size: 22px;
    }
}
</style>