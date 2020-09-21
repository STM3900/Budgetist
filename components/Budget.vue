<template>
    <v-container v-resize="onResize" :class="`${padding}`">
        <v-card class="mx-auto blue white--text">
            <v-card-title>Mon budget :</v-card-title>
            <v-card-subtitle class="display-1 white--text">{{budget}}{{devise}}</v-card-subtitle>
        </v-card>
    </v-container>
</template>

<script>
    export default {
        name: "budget",
        props: ['budget', 'devise'],
        data: () => ({
            windowSize: {
                x: 0,
                y: 0,
            },

            padding: ''
        }),
        mounted () {
            this.onResize()
        },
        methods: {
            onResize () {
                this.windowSize = { x: window.innerWidth, y: window.innerHeight };
                this.setPadding();
            },
            setPadding () {
                if(this.windowSize.x < 600){
                    this.padding = 'pr-0 pl-0';
                }
                else{
                    this.padding = 'pl-0';
                }
            }
        },
    };
</script>