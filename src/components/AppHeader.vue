<script>
import { store } from '../store';


export default {
    name: 'AppHeader',
    data() {
        return {
            store,
        }
    },
    methods: {

    }
}

</script>

<template>
    <div class="container-fluid">
        <div class="row">
            <div class="col-12">
                <h1 class="text-danger">BoolFlix</h1>
            </div>
            <div class="row">
                <div class="col-sm-12 col-md-3">
                    <div class="input-group mb-3">
                        <input type="text" class="form-control" v-model="store.searchMovie"
                            @keyup.enter="$emit('search', store.searchMovie)" placeholder="Search movies or tv show"
                            aria-label="Search movies or tv show" aria-describedby="button-addon2">
                        <button @click="$emit('search', store.searchMovie)"
                            class="btn btn-outline-secondary btn-danger text-dark fw-5 " type="button"
                            id="button-addon2">Search</button>
                    </div>
                </div>
            </div>
            <div class="row list-movies">
                <div class="col-sm-12">
                    <ul>
                        <li v-for="movieElement in store.moviesData">
                            <h3> {{ movieElement.original_title }}</h3>
                            <h4> {{ movieElement.title }}</h4>
                            <h5>Original language : {{ movieElement.original_language }}</h5>
                            <h5>Vote average : {{ movieElement.vote_average }} stars</h5>
                        </li>
                    </ul>
                </div>
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
</style>