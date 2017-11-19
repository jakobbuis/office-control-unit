<template>
    <table class="table is-striped is-narrow is-fullwidth">
        <tbody>
            <room v-for="room in rooms" :room="room" key="room.room" @override="updateOverride"></room>
        </tbody>
    </table>
</template>

<script>
import Room from './Room.vue';

export default {

    components: { Room },

    data() {
        return {
            socket: new WebSocket('ws://klimaat:5546'),
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
            this.$parent.$emit('connection', false);
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
</style>
