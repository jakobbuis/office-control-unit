<template>
    <div class="box">
        <h2>Meeting room lights</h2>

        <table class="table is-striped is-narrow is-fullwidth">
            <tbody>
                <tr>
                    <td>
                        <div class="field">
                            <input id="switch_maaskamer" type="checkbox" name="switch_maaskamer" class="switch is-rounded is-rtl" checked="checked">
                            <label for="switch_maaskamer"></label>
                        </div>
                    </td>
                    <td>Maaskamer</td>
                    <td class="indicator"><span class="colour"></span></td>
                </tr>
                <tr>
                    <td>
                        <div class="field">
                            <input id="switch_podiumkamer" type="checkbox" name="switch_podiumkamer" class="switch is-rounded is-rtl" checked="checked">
                            <label for="switch_podiumkamer"></label>
                        </div>
                    </td>
                    <td>Podiumkamer</td>
                    <td class="indicator"><span class="colour"></span></td>
                </tr>
                <tr>
                    <td>
                        <div class="field">
                            <input id="switch_spreekkamer" type="checkbox" name="switch_spreekkamer" class="switch is-rounded is-rtl" checked="checked">
                            <label for="switch_spreekkamer"></label>
                        </div>
                    </td>
                    <td>Spreekkamer</td>
                    <td class="indicator"><span class="colour"></span></td>
                </tr>
            </tbody>
        </table>
    </div>
</template>

<script>
export default {
}
</script>

<style scoped>
.table {
    margin-bottom: 0;
}

.colour {
    display: block;
    background-color: red;
    width: 1.5em;
    height: 1.5em;
    border-radius: 50%;
    margin: 0 auto;
}

.indicator {
    padding: 0;
}
</style>
