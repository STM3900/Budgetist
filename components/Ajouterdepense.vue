<template>
  <v-card class="mx-auto">
    <v-form ref="form" v-on:submit.prevent="submit" v-model="valid" class="pa-10">
      <v-text-field type="number" label="Montant de la dépense" v-model="newMontantC" :rules="isNum" prepend-icon="euro"></v-text-field>
      <v-text-field label="Description de la dépense" v-model="newTexteC" :rules="isEmpty" prepend-icon="edit">></v-text-field>
      <v-radio-group row v-model="newType" :rules="isEmpty">
        <v-radio label="Alimentation" value="local_grocery_store"></v-radio>
        <v-radio label="Loisir" value="mood"></v-radio>
        <v-radio label="Transport" value="directions_bus"></v-radio>
        <v-radio label="Imprévu" value="warning"></v-radio>
      </v-radio-group>
      <v-btn :disabled="!valid" type="submit" class="success mt-5">Ajouter dépense !</v-btn>
    </v-form>
  </v-card>
</template>

<script>
export default {
    name: 'Ajouterdepense',
    data: function(){
        return{
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
      submit () {
        if(this.$refs.form.validate()){
          console.log(this.newMontantC, this.newTexteC);
          this.$emit('submit', this.newMontantC, this.newTexteC, this.newType);
          console.log(this.newType);
          this.$refs.form.reset();
        }
    }
  }
};
</script>