<template>
    <tr>
        <td>
            <div class="field">
                <input :id="room.room" type="checkbox" :name="room.room" class="switch is-rounded is-rtl" :checked="room.endOverride == null" @change="updateOverride">
                <label :for="room.room"></label>
            </div>
        </td>
        <td>{{ room.room }}</td>
    </tr>
</template>

<script>
export default {

    props: ['room'],

    methods: {
        updateOverride(event) {
            const midnight = new Date;
            midnight.setHours(24, 0, 0, 0);
            this.$emit('override', {
                name: this.room.room,
                override: this.room.endOverride ? null : midnight,
            });
        }
    },
};
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
