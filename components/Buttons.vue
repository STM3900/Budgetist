<template>
     <v-container>
      <v-col align="center">
        <v-col sm="6">
          <nuxt-link to="budget"><v-btn color="info" block outlined><v-icon left>arrow_right_alt</v-icon>Aller au budget</v-btn></nuxt-link> 
        </v-col>
        <v-col sm="6">
            <v-dialog v-model="dialog" max-width="550px">
                <template v-slot:activator="{ on, attrs }">
                <v-btn color="warning" outlined block v-bind="attrs" v-on="on"><v-icon left>delete</v-icon>Réinitialiser votre profil</v-btn>
                </template>
                <v-card>
                <v-card-title class="headline error white--text"><v-icon left color="white">warning</v-icon>Êtes-vous sur ?</v-card-title>
                <v-card-text class="pt-5 pb-3">Cela supprimera définitivement toutes vos dépenses. Continuer ?</v-card-text>
                <v-card-actions class="pt-0">
                    <v-btn color="error" text @click="dialog = false, $emit('reset')">Oui</v-btn>
                    <v-spacer></v-spacer>
                    <v-btn color="info" text @click="dialog = false">Noooon</v-btn>
                </v-card-actions>
                </v-card>
            </v-dialog>
        </v-col>
      </v-col>
    </v-container>
</template>

<script>
export default {
    name: 'Buttons',
    data: function(){
        return{
            dialog: false
        }
    }
}
</script>