<template>
    <v-card class="mx-auto">
        <v-row justify="space-between" align="center" class="mb-0">
            <v-col sm="8" class="mt-0 mb-0"> 
                <v-row justify="start" align="center" class="mb-0">
                    <v-col sm='1' class="mt-0 mb-0 mr-n3 ml-4 pa-0" align="center">
                        <v-icon large>{{icone}}</v-icon>
                    </v-col>
                    <v-col class="mt-0 mb-0 pa-0">
                        <v-card-title class="pt-0 pb-0 mt-0 mb-3 text-capitalize">{{texteDepense}}</v-card-title>
                        <v-card-subtitle class="pb-0 mb-0">{{date}}</v-card-subtitle>                    
                    </v-col>                    
                </v-row>
            </v-col>
            <v-col sm="4" align="end" class="pt-0 pb-0 mt-0 mb-0">
                <v-card-text class="headline pt-0 pb-0 p">{{montantDepense}}{{devise}}</v-card-text>
            </v-col>
        </v-row>
        <v-card-actions class="mt-0"><v-btn v-on:click="$emit('suppr')" depressed small class="error"><v-icon left>clear</v-icon>Supprimer dépense</v-btn></v-card-actions>
    </v-card>
</template>

<script>
export default {
    transition: 'fade',
    name: "depense",
    props: [
        'numDepense',
        'montantDepense',
        'texteDepense',
        'devise',
        'date',
        'icone'
    ]
}
</script>

<style scoped>
    div{
        margin-top: 5px;
        margin-bottom: 15px;
    }
</style>