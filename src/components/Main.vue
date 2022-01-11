<template>
    <main>
        <div class="container">
            <div v-if="!isLoadingApi" class="discs-list">
                <DiscCard v-for="(disc, index) in filteredDiscs" :key="index" :details="disc" />
            </div>
            <div v-else>
                <Loader />
            </div>
        </div>
    </main>
</template>

<script>
import axios from 'axios';
import DiscCard from "./DiscCard.vue";
import Loader from "./Loader.vue";
export default {
    name: "Main",
    components: {
        DiscCard,
        Loader
    },
    props: {
        filterGenre: String
    },
    data: function() {
        return {
            discsList: [],
            isLoadingApi: true,
            genresList: []
        };
    },
    methods: {
        getDiscs: function() {
            axios.get('https://flynn.boolean.careers/exercises/api/array/music')
            .then((response) => {
                this.discsList = response.data.response;
                // Creo array generi
                this.discsList.forEach((element) => {
                    if(!this.genresList.includes(element.genre)) {
                       this.genresList.push(element.genre); 
                    }
                });
                this.$emit('genresListCreated', this.genresList);
                this.isLoadingApi = false;
            });
        }
    },
    computed: {
        filteredDiscs: function() {
            // Se l'utente seleziona tutti i generi
            if(this.filterGenre === '') {
                return this.discsList;
            }
            // Altrimenti se l'utente seleziona un genere
            let filteredArray = [];
            filteredArray = this.discsList.filter((element) => {
                return element.genre === this.filterGenre;
            });
            return filteredArray;
        }
    },
    created: function() {
        this.getDiscs();
    }
}
</script>

<style scoped lang="scss">
@import '../styles/variables.scss';
main {
    overflow-y: auto;
    padding: 40px 0;
    background-color: $secondary_color;
    height: calc(100% - 70px);
    color: white;
    .discs-list {
        display: flex;
        flex-wrap: wrap;
    }
}
</style>