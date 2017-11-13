<template>
    <div id="app">
        <nav class="navbar is-warning">
            <div class="navbar-brand">
                <h1 class="navbar-item">
                    Office Control Unit
                </h1>
            </div>
        </nav>

        <div class="container">
            <div class="tile is-ancestor">
                <div class="tile is-3">
                    <klimaat></klimaat>
                </div>
                <div class="tile is-9">
                    <public-address></public-address>
                </div>
            </div>
        </div>

    </div>
</template>

<script>
import Klimaat from './components/Klimaat/Klimaat.vue';
import PublicAddress from './components/PublicAddress.vue';

export default {
    name: 'app',
    components: {Klimaat, PublicAddress},
}
</script>

<style lang="scss">
@import './node_modules/bulma/bulma.sass';
@import './node_modules/bulma-switch/switch.sass';

.tile {
    padding: 1em;
}

.box {
    width: 100%;
    padding: 0;

    h2 { // Component headings
        font-weight: bold;
        background-color: #666;
        padding: 0.25em 0.5em;
        color: white;
    }
}

</style>
