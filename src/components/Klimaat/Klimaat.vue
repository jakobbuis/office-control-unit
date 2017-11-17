<template>
    <div class="box">
        <h2>Meeting room lights</h2>

        <div class="notification is-danger" v-if="!connected">
            Verbinding maken met klimaat is mislukt. Heb je wel verbinding met
            de IN10-WiFi?
        </div>


        <table class="table is-striped is-narrow is-fullwidth" v-if="connected">
            <tbody>
                <room v-for="room in rooms" :room="room" key="room.room" @override="updateOverride"></room>
            </tbody>
        </table>
    </div>
</template>

<script>
import Room from './Room.vue';

export default {

    components: { Room },

    data() {
        return {
            socket: new WebSocket('ws://klimaat:5546'),
            connected: true,
            rooms: [],
        };
    },

    created() {
        this.socket.onmessage = (message) => {
            this.rooms = JSON.parse(message.data).sort((a, b) => {
                return a.room.localeCompare(b.room);
            });
        };
        this.socket.onerror = (message) => {
            this.connected = false;
        };
    },

    methods: {
        updateOverride({name, override}) {
            // Update the right room
            let target = this.rooms.filter((room) => {
                return room.room === name;
            });
            target.endOverride = override;

            // Emit the new state
            const message = JSON.stringify(this.state);
            this.socket.send(message);
        }
    },
}
</script>

<style scoped>
.table {
    margin-bottom: 0;
}

.notification {
    padding: 1em;
    border-radius: 0;
}
</style>
