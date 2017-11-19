<template>
    <div class="box">
        <h2>{{ title }}</h2>

        <div class="notification is-danger" v-show="!connected">
            Verbinding mislukt
        </div>

        <div class="content" v-show="connected">
            <slot></slot>
        </div>
    </div>
</template>

<script>
export default {

    props: ['title'],

    data() {
        return {
            connected: true,
        };
    },

    created() {
        this.$on('connection', this.setConnectionStatus);
    },

    methods: {
        setConnectionStatus(status) {
            this.connected = status;
        },
    },
};
</script>

<style lang="scss" scoped>
.box {
    width: 100%;
    padding: 0;

    h2 { // Component headings
        font-weight: bold;
        background-color: #666;
        padding: 0.25em 0.5em;
        color: white;
    }

    &> .notification {
        padding: 0.5em 1em 0 1em;
        border-radius: 0;
        height: 100%;
    }
}
</style>
