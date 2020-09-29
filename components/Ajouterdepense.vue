<template>
  <v-dialog max-width="700px" v-model="dialog">
    <template v-slot:activator="{on, attrs}">
      <v-btn color="info" class="mr-3" :depressed='depressedState' block v-bind="attrs" v-on="on"><v-icon left>add</v-icon>Ajouter une dépense</v-btn>
    </template>
    <v-card class="mx-auto">
      <v-form ref="form" v-on:submit.prevent="submit" v-model="valid" class="pa-10">
        <v-text-field type="number" label="Montant de la dépense" v-model="newMontantC" :rules="isNum" prepend-icon="euro"></v-text-field>
        <v-text-field label="Description de la dépense" v-model="newTexteC" :rules="isEmpty" prepend-icon="edit">></v-text-field>
        <v-radio-group row v-model="newType" :rules="isEmpty">
          <v-radio label="Alimentation" value="local_grocery_store"></v-radio>
          <v-radio label="Loisir" value="emoji_emotions"></v-radio>
          <v-radio label="Transport" value="directions_bus"></v-radio>
          <v-radio label="Autre" value="pending"></v-radio>
          <v-radio label="Imprévu" value="report_problem"></v-radio>
        </v-radio-group>
        <v-card-actions>
          <v-row justify="space-between">
            <v-col md="3" sm="12">
              <v-btn :disabled="!valid" type="submit" class="success" block><v-icon left>add</v-icon>Ajouter dépense</v-btn>
            </v-col>
            <v-col md="3" sm="12">
              <v-btn color="error" outlined v-on:click="dialog = false" block><v-icon left>clear</v-icon>Annuler</v-btn>
            </v-col>
          </v-row>
        </v-card-actions>
      </v-form>
    </v-card>
  </v-dialog>
</template>

<script>
export default {
    name: 'Ajouterdepense',
    props: ['depressedState'],
    data: function(){
        return{
            dialog: false,

            valid: false,

            newMontantC: '',
            newTexteC: '',
            newType: '',


            isNum: [
              v => !isNaN(v) || 'La valeur doit être un nombre.',
              v => !!v || 'Champ requis.',
              v => v > 0 || 'La valeur ne peut être négative.'
            ],
            isEmpty: [
              v => !!v || 'Champ requis.'
            ]
        }
    },
    methods: {
      submit() {
        if(this.$refs.form.validate()){
          const data = {
            montant: this.newMontantC,
            texte: this.newTexteC,
            type: this.newType,
          }
          this.$emit('submit', data);
          this.$refs.form.reset();
          this.dialog = false;
        }
    }
  },
  watch: {
    dialog(val){
      !val && this.$refs.form.reset();
    }
  }
};
</script>