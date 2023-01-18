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
    <div class="container-fluid d-flex justify-content-between align-items-center">
        <div class="row">
            <div class="col-12">
                <h1 class="text-danger">BoolFlix</h1>
            </div>
        </div>
        <div class="row">
            <div class="col-sm-12 col-md-12">
                <div class="input-group mb-3">
                    <!-- utilizzo v-model per creare una relazione tra l'input e la proprietà searchMovie di store.js,
                    quindi quando si digita qualcosa nell'input si aggiorna automaticamente il valore di searchMovie in
                    store.js.Quando si preme enter o si clicca sul bottone search si emette un evento chiamato 'search' con argomento store.searchMovie. Questo evento è utilizzato in App.vue per effettuare la ricerca -->
                    <input type="text" class="form-control" v-model="store.searchMovie"
                        @keyup.enter="$emit('search', store.searchMovie)" placeholder="Search movies or tv show"
                        aria-label="Search movies or tv show" aria-describedby="button-addon2">
                    <button @click="$emit('search', store.searchMovie)"
                        class="btn btn-outline-secondary btn-danger text-dark fw-5 " type="button"
                        id="button-addon2">Search</button>
                </div>
            </div>
        </div>
    </div>
</template>


<style lang="scss" scoped>
@use '../styles/general.scss' as *;
@use '../styles/partials/variables' as *;
@import 'bootstrap/scss/bootstrap.scss';

div.input-group {
    vertical-align: bottom;
}
</style>