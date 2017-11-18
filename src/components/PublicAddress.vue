<template>
    <div class="box">
        <h2>Sonos public address system</h2>
        <form action="#" @submit.prevent="address">
            <div class="field has-addons">
                <p class="control">
                    <span class="select">
                        <select v-model="selectedZone">
                            <option v-for="zone in zones">{{ zone }}</option>
                        </select>
                    </span>
                </p>
                <p class="control is-expanded">
                    <input class="input" type="text" placeholder="Message" v-model="message">
                </p>
                <p class="control">
                    <button type="submit" class="button is-primary">Send</button>
                </p>
            </div>
        </form>
    </div>
</template>

<script>
import axios from 'axios';

export default {

    data() {
        return {
            zones: [],
            selectedZone: null,
            message: '',
        };
    },

    created() {
        axios.get('http://klimaat:5005/zones').then((response) => {
            this.zones = response.data.map((zone) => {
                return zone.coordinator.roomName;
            });
            this.selectedZone = this.zones[0];
        });
    },

    methods: {
        address() {
            const zone = encodeURIComponent(this.selectedZone);
            const message = encodeURIComponent(`Mededeling: ${this.message}. Herhaling: ${this.message}`);
            axios.get(`http://klimaat:5005/${zone}/say/${message}/nl`);
        }
    },
};
</script>

<style scoped>
form {
    padding: 1em;
}
</style>
