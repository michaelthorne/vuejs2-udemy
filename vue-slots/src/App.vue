<template>
    <div class="container">
        <div class="row">
            <div class="col-sm">
                <br>
                <button @click="selectedComponent = 'appQuote'">Quote</button>
                <button @click="selectedComponent = 'appAuthor'">Author</button>
                <button @click="selectedComponent = 'appNew'">New</button>
                <hr>
                <p>{{ selectedComponent }}</p>
                <hr>
                <keep-alive>
                    <component :is="selectedComponent"></component>
                </keep-alive>
                <!--<app-quote>
                    <h2 slot="title">{{ quoteTitle }}</h2>
                    <span slot="subtitle">Subtitle goes here.</span>
                    <p>The contents of my quote</p>
                </app-quote>-->
            </div>
        </div>
    </div>
</template>

<script>
    import Quote from './components/Quote.vue';
    import Author from './components/Author.vue';
    import New from './components/New.vue';

    export default {
        components: {
            appQuote: Quote,
            appAuthor: Author,
            appNew: New,
        },
        data () {
            return {
                selectedComponent: 'appQuote',
                quoteTitle: 'This is the title of my quote'
            }
        }
    }
</script>

<style>

</style>
