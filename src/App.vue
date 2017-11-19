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
                    <box title="Meeting room lights">
                        <klimaat></klimaat>
                    </box>
                </div>
                <div class="tile is-9">
                    <box title="Sonos public address system">
                        <public-address></public-address>
                    </box>
                </div>
            </div>
        </div>

    </div>
</template>

<script>
import Box from './components/Box.vue';
import Klimaat from './components/Klimaat/Klimaat.vue';
import PublicAddress from './components/PublicAddress.vue';

export default {
    name: 'app',
    components: {Box, Klimaat, PublicAddress},
}
</script>

<style lang="scss">
@import './node_modules/bulma/bulma.sass';
@import './node_modules/bulma-switch/switch.sass';

.tile {
    padding: 1em;
}
</style>
