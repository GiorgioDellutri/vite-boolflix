<script>
import { store } from '../store';


export default {
    name: 'AppMain',
    data() {
        return {
            store,
            flags: ['it', 'en', 'es', 'fr']
        }
    },
    methods: {
        getImagePath: function (imgPath) {
            return new URL(`../assets/img/${imgPath}.png`, import.meta.url).href
        }
    },
    computed: {
        posterUrl() {
            return "https://image.tmdb.org/t/p/w342" + this.data.poster_path
        }
    }
}
</script>

<template>
    <div class="container-fluid">
        <div class="row">
            <div class="col-sm-12 col-md-3">
                <div class="input-group mb-3">
                    <input type="text" class="form-control" v-model="store.searchMovie"
                        @keyup.enter="$emit('search', store.searchMovie)" placeholder="Search movies or tv show"
                        aria-label="Search movies or tv show" aria-describedby="button-addon2">
                    <button @click="$emit('search', store.searchMovie, store.searchMovie)"
                        class="btn btn-outline-secondary btn-danger text-dark fw-5 " type="button"
                        id="button-addon2">Search</button>
                </div>
            </div>
        </div>
        <div class="row list-movies">
            <div class="col-sm-12">
                <ul>
                    <li v-for="movieElement in store.moviesData">
                        <h1>Movies:</h1>
                        <img :src="posterUrl">
                        <h3> {{ movieElement.original_title }}</h3>
                        <h4> {{ movieElement.title }}</h4>
                        <h5 class="d-inline">Language</h5>
                        <img :src="getImagePath(movieElement.original_language)" alt="flag">
                        <h5>Vote average : {{ movieElement.vote_average }} stars</h5>
                    </li>
                </ul>
                <ul>
                    <li v-for="seriesElement in store.tvShowData">
                        <h1>Tv series:</h1>
                        <h3> {{ seriesElement.original_name }}</h3>
                        <h4> {{ seriesElement.name }}</h4>
                        <h5 class="d-inline">Language</h5>
                        <img :src="getImagePath(seriesElement.original_language)" alt="flag">
                        <h5>Vote average : {{ seriesElement.vote_average }} stars</h5>
                    </li>
                </ul>
            </div>
        </div>
    </div>
</template>


<style lang="scss" scoped>
@use '../styles/general.scss' as *;
@use '../styles/partials/variables' as *;
@import 'bootstrap/scss/bootstrap.scss';

ul li {
    list-style: none;
    padding: 0;
}

div.list-movies img {
    width: 20px;
    margin-left: 10px;
    vertical-align: bottom;
}
</style>