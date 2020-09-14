<template>
    <v-container class="pl-0">
        <v-card class="mx-auto blue white--text">
            <v-card-title>Mon budget :</v-card-title>
            <v-card-subtitle class="display-1 white--text">{{budget}}{{devise}}</v-card-subtitle>
        </v-card>
    </v-container>
</template>

<script>
    export default {
        name: "budget",
        props: ['budget', 'devise']
    };
</script>