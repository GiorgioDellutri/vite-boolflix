<script>
import { store } from '../store';



export default {
    name: 'AppMain',
    data() {
        return {
            store,
            flags: ['it', 'en', 'es', 'fr'],
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
        },
    },
}
</script>

<template>
    <div class="container-fluid px-5 py-3">
        <div class="row  list-movies">
            <div class="col-sm-12 col-md-12 col-lg-12 d-flex flex-wrap justify-content-evenly">
                <!-- MOVIES -->
                <!-- effettuo il ciclo v-for che permette di visualizzare i film e serie tv  con i propri dati -->
                <div v-for="movieElement in store.moviesData" class="card m-3" style="width: 18rem;">
                    <!-- utilizzo il metodo getImageUrl per generare l'url e lo passo come parametro al metodo per
                        generare l'url dell'immagine e poi lo utilizzo come src dell'immagine. In questo modo, posso
                        utilizzare il metodo "getImagePath" per generare l'URL dell'immagine in base al valore di
                        "poster_path" di ogni elemento del ciclo v-for e utilizzarlo come "src" per visualizzare
                        l'immagine nella pagina.Stesso discorso per le serie tv -->
                    <img class="cover-image" v-if="movieElement.poster_path"
                        :src="getImageUrl(movieElement.poster_path)" />
                    <div class="card-body">
                        <h3> {{ movieElement.original_title }}</h3>
                        <h4> {{ movieElement.title }}</h4>
                        <h5 class="d-inline">Language</h5>
                        <!-- nell'immagine passo come src il metodo getImagePath per generare l'url dell'immagine della
                        bandiera. Cosi visualizzo l'immagine della bandiera relativa al linguaggio originale del fil o
                        della serie tv -->
                        <img class="flag-language" :src="getImagePath(movieElement.original_language)" alt="flag">
                        <p>Rating Movie: <i class="fa-regular fa-star"
                                v-for="n in Math.ceil(movieElement.vote_average / 2)"></i>
                            <i class="fa-regular fa-star"
                                v-for="n in Math.floor(5 - (movieElement.vote_average / 2))"></i>
                        </p>
                    </div>
                </div>
                <!-- TV SERIES -->
                <div v-for="seriesElement in store.tvShowData" class="card" style="width: 18rem;">
                    <img class=" cover-image" v-if="seriesElement.poster_path"
                        :src="getImageUrl(seriesElement.poster_path)" />
                    <div class="card-body">
                        <h3> {{ seriesElement.original_name }}</h3>
                        <h4> {{ seriesElement.name }}</h4>
                        <h5 class="d-inline">Language</h5>
                        <img class="flag-language" :src="getImagePath(seriesElement.original_language)" alt="flag">
                        <p>Rating Movie: <i class="fa-regular fa-star"
                                v-for="n in Math.ceil(seriesElement.vote_average / 2)"></i>
                            <i class="fa-regular fa-star"
                                v-for="n in Math.floor(5 - (seriesElement.vote_average / 2))"></i>
                        </p>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>


<style lang="scss" scoped>
@use '../styles/general.scss' as *;
@use '../styles/partials/variables' as *;
@import 'bootstrap/scss/bootstrap.scss';
@import 'font-awesome/css/font-awesome.css';

ul li {
    list-style: none;
    padding: 0;
}

div.list-movies img.flag-language {
    width: 20px;
    margin-left: 10px;
    vertical-align: bottom;
}

.container:hover .overlay {
    opacity: 1;

    .text {
        color: white;
        font-size: 20px;
        position: absolute;
        top: 50%;
        left: 50%;
        -webkit-transform: translate(-50%, -50%);
        -ms-transform: translate(-50%, -50%);
        transform: translate(-50%, -50%);
        text-align: center;
    }
}
</style>