<template>
    <div class="box">
        <h2>Meeting room lights</h2>

        <div class="notification is-danger" v-if="!connected">
            Verbinding maken met klimaat is mislukt. Heb je wel verbinding met
            de IN10-WiFi?
        </div>


        <table class="table is-striped is-narrow is-fullwidth" v-if="connected">
            <tbody>
                <room v-for="room in rooms" key="room.room"></room>
            </tbody>
        </table>
    </div>
</template>

<script>
export default {

    data() {
        return {
            connected: true,
            rooms: []
        };
    },

    created() {
        const socket = new WebSocket('ws://klimaat:5546');
        socket.onmessage = (message) => {
            this.rooms = JSON.parse(message.data).sort((a, b) => {
                return a.room.localeCompare(b.room);
            });
        };
        socket.onerror = (message) => {
            this.connected = false;
        };
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
