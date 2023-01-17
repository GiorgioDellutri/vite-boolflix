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
        </div>
    </div>
</template>


<style lang="scss" scoped>
@use '../styles/general.scss' as *;
@use '../styles/partials/variables' as *;
@import 'bootstrap/scss/bootstrap.scss';
</style>