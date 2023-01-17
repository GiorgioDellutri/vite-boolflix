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
        //creo un  metodo  per generare l'URL dell'immagine delle bandiere.Il metodo accetta un parametro "imgPath" che rappresenta il nome del file dell'immagine della bandiera.Utilizza l'oggetto URL per generare un URL assoluto utilizzando "../assets/img/${imgPath}.png" come percorso relativo alla directory corrente del progetto e "import.meta.url" come base per generare l'URL assoluto.
        getImagePath: function (imgPath) {
            return new URL(`../assets/img/${imgPath}.png`, import.meta.url).href
        },
        //creo un metodo per generare l'URL dell'immagine
        getImageUrl: function (imgPath) {
            return "https://image.tmdb.org/t/p/w300" + imgPath  //utilizzo la base dell'url e aggiungo la dimensione w300 all'url
        }
    },
    computed: {
        // utilizzo una proprietà computata chiamata "posterUrl" per generare l'URL dell'immagine, con un ternario controllo se l'oggetto "store.moviesData" esiste.Se esiste, utilizza il valore di "poster_path" per generare l'URL completo dell'immagine utilizzando "https://image.tmdb.org/t/p/w342" come base dell'URL e la dimensione dell'immagine "w342". In caso contrario, restituisce una stringa vuota.
        posterUrl() {
            return store.moviesData ? "https://image.tmdb.org/t/p/w342" + store.moviesData.poster_path : ''
        }
    },
}
</script>

<template>
    <div class="container-fluid">
        <div class="row">
            <div class="col-sm-12 col-md-3">
                <div class="input-group mb-3">
                    <!-- utilizzo v-model per creare una relazione tra l'input e la proprietà searchMovie di store.js,
                    quindi quando si digita qualcosa nell'input si aggiorna automaticamente il valore di searchMovie in
                    store.js. -->

                    <!-- quando si preme enter o si clicca sul bottone search si emette un evento chiamato search con due argomenti store.searchMovie e store.searchMovie. Questo evento è utilizzato in App.vue per effettuare la ricerca -->
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
                <!-- MOVIES -->
                <ul>
                    <!-- effettuo il ciclo v-for che permette di visualizzare i film con i propri dati -->
                    <li v-for="movieElement in store.moviesData">
                        <!-- <h1>Movies:</h1> -->
                        <!-- utilizzo il metodo getImageUrl per generare l'url e lo passo come parametro al metodo per
                        generare l'url dell'immagine e poi lo utilizzo come src dell'immagine. In questo modo, posso
                        utilizzare il metodo "getImagePath" per generare l'URL dell'immagine in base al valore di
                        "poster_path" di ogni elemento del ciclo v-for e utilizzarlo come "src" per visualizzare
                        l'immagine nella pagina.Stesso discorso per le serie tv -->
                        <img v-if="movieElement.poster_path" :src="getImageUrl(movieElement.poster_path)" />
                        <h3> {{ movieElement.original_title }}</h3>
                        <h4> {{ movieElement.title }}</h4>
                        <h5 class="d-inline">Language</h5>
                        <!-- nell'immagine passo come src il metodo getImagePath per generare l'url dell'immagine della bandiera. Cosi visualizzo l'immagine della bandiera relativa al linguaggio originale del fil o della serie tv -->
                        <img class="flag-language" :src="getImagePath(movieElement.original_language)" alt="flag">
                        <h5>Vote average : {{ movieElement.vote_average }} stars</h5>
                    </li>
                </ul>
                <!-- TV SERIES -->
                <ul>
                    <li v-for="seriesElement in store.tvShowData">
                        <!-- <h1>Tv series:</h1> -->
                        <img v-if="seriesElement.poster_path" :src="getImageUrl(seriesElement.poster_path)" />
                        <h3> {{ seriesElement.original_name }}</h3>
                        <h4> {{ seriesElement.name }}</h4>
                        <h5 class="d-inline">Language</h5>
                        <img class="flag-language" :src="getImagePath(seriesElement.original_language)" alt="flag">
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

div.list-movies img.flag-language {
    width: 20px;
    margin-left: 10px;
    vertical-align: bottom;
}
</style>