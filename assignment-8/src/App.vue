<template>
    <div class="container">
        <div class="row">
            <div class="col-sm">
                <br>
                <button @click="selectedComponent = 'appBlue'" class="btn btn-primary">Load Blue Template</button>
                <button @click="selectedComponent = 'appGreen'" class="btn btn-success">Load Green Template</button>
                <button @click="selectedComponent = 'appRed'" class="btn btn-danger">Load Red Template</button>
                <hr>
                <component :is="selectedComponent">
                    <h2>{{ selectedComponent }}</h2>
                </component>
                <!--<app-blue></app-blue>
                <app-green></app-green>
                <app-red></app-red>-->
            </div>
        </div>
    </div>
</template>

<script>
    import Blue from './components/Blue.vue';
    import Green from './components/Green.vue';
    import Red from './components/Red.vue';

    export default {
        data () {
            return {
                selectedComponent: 'appBlue'
            }
        },
        components: {
            appBlue: Blue,
            appGreen: Green,
            appRed: Red,
        }
    }
</script>

<style lang="scss">

</style>
