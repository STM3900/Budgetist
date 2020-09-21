<template>
    <v-container>
        <v-card :class="`${couleur} white--text mx-auto`">
            <v-card-title>Montant restant :</v-card-title>
            <v-card-subtitle class="display-1 white--text">{{reste}}{{devise}}</v-card-subtitle>
        </v-card>
    </v-container>
</template>

<script>
export default {
    name: 'Reste',
    props: ['reste','devise','couleur']
}
</script>