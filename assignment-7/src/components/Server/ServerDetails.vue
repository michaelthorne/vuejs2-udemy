<template>
    <div class="col-xs-12 col-sm-6">
        <p v-if="!server">Please select a server</p>
        <p v-else>
            Server #{{ server.id }}: {{ server.status }}
            <template v-if="server.status != 'Normal'">
                <hr>
                <button @click="resetStatus">Change to Normal</button>
            </template>
        </p>
    </div>
</template>

<script>
    import {serverBus} from '../../main';

    export default {
        data () {
            return {
                server: null
            }
        },
        created () {
            serverBus.$on('serverSelected', (server) => {
                this.server = server;
            });
        },
        methods: {
            resetStatus () {
                this.server.status = 'Normal';
            }
        }
    }
</script>

<style>

</style>
