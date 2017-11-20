<template>
    <div class="content">
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
        <div class="status" v-if="status != null">
            <div>
                <i class="fa fa-fw" :class="statusClass"></i>
                {{ statusMessage }}
            </div>
        </div>
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
            status: null,
            lastError: null,
        };
    },

    computed: {
        statusMessage() {
            if (this.status === 'sending') {
                return 'Playing message';
            }
            if (this.status === 'success') {
                return 'Message delivered';
            }
            if (this.status === 'error') {
                return `Error: ${this.lastError}`;
            }
        },

        statusClass() {
            if (this.status === 'sending') {
                return 'fa-circle-o-notch fa-spin';
            }
            if (this.status === 'success') {
                return 'fa-check';
            }
            if (this.status === 'error') {
                return 'fa-times';
            }
        },
    },

    created() {
        axios.get('http://klimaat:5005/zones').then((response) => {
            this.zones = response.data.map((zone) => {
                return zone.coordinator.roomName;
            });
            this.selectedZone = this.zones[0];
        }).catch(() => this.$parent.$emit('connection', false));
    },

    methods: {
        address() {
            this.status = 'sending';

            const volume = 40;
            const zone = encodeURIComponent(this.selectedZone);
            const message = encodeURIComponent(`${this.message}. Herhaling: ${this.message}.`);

            // Play NS sound
            axios.get(`http://klimaat:5005/${zone}/clip/ns.mp3/${volume}`).then(() => {
                // Play message
                axios.get(`http://klimaat:5005/${zone}/say/${message}/nl/${volume}`).then((response) => {
                    this.status = response.data.status;
                }).catch((error) => {
                    if (error.response) {
                        this.status = error.response.data.status;
                        this.lastError = error.response.data.error;
                    }
                    else {
                        this.status = 'error';
                        this.lastError = 'unknown error occurred';
                    }
                });
            });
        },
    },
};
</script>

<style lang="scss" scoped>
.content {
    padding: 1em;
}
.status {
    font-style: italic;

    .fa-check { color: green; }
    .fa-times { color: red; }
}
</style>
