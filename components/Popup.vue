<template>
    <v-dialog max-width="600px">
        <template v-slot:activator="{on, attrs}">
            <v-btn class="success" v-bind="attrs" v-on="on">Activer la popup</v-btn>
        </template>
        <v-card>
            <v-card-title>
                <h1>Coucou !</h1>
            </v-card-title>
            <v-card-text>
                <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Vel, saepe laborum harum repellat praesentium temporibus facilis! Libero est ab doloremque nemo praesentium fuga incidunt odio ullam illo! Reiciendis, laborum quae?</p>
            </v-card-text>
        </v-card>
    </v-dialog>
</template>

<script>
export default {
    name: 'popup',
    data: function(){
        return{
            dialog: false,
        }
    }
}
</script>