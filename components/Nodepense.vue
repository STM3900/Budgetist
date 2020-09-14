<template>
    <div>
        <v-alert prominent text outlined type="info">
            <v-row align="center">
                <v-col class="grow">Pas de dépenses ! Ajoutez-en une en cliquant sur le bouton</v-col>
                <v-col class="shrink">
                <AjouterDepense  v-on:submit="$emit('submit', $event)" :depressedState="true"/>
                </v-col>
            </v-row>
        </v-alert>
    </div>
</template>

<script>
import AjouterDepense from "../components/AjouterDepense";

export default {
    components: { AjouterDepense },
    name: 'Nodepense',
}
</script>