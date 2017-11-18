<template>
    <div class="box">
        <h2>Sonos public address system</h2>
        <form action="#">
            <div class="field has-addons">
                <p class="control">
                    <span class="select">
                        <select>
                            <option>Activate</option>
                            <option>Developers</option>
                            <option>Producers</option>
                        </select>
                    </span>
                </p>
                <p class="control is-expanded">
                    <input class="input" type="text" placeholder="Message">
                </p>
                <p class="control">
                    <a class="button is-primary">
                        Send
                    </a>
                </p>
            </div>
        </form>
    </div>
</template>

<script>
export default {

};
</script>

<style scoped>
form {
    padding: 1em;
}
</style>
