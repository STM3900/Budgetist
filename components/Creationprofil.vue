<template>
    <v-form ref="form" v-on:submit.prevent="submit" v-model="valid">
      <v-container>
        <v-col align="center">
          <v-col sm="8">
            <v-text-field type="text" label="Entrez votre nom" v-model="name" :rules="isEmpty" append-icon="account_circle"></v-text-field>
          </v-col>
          <v-col sm="8">
            <v-text-field type="number" label="Entrez votre budget" v-model="budget" :rules="isNum" append-icon="euro"></v-text-field>
          </v-col>
          <v-col sm="8" align="start">
            <v-btn :disabled="!valid" type="submit" class="success" ><v-icon left>call_made</v-icon>C'est parti !</v-btn>
          </v-col>
        </v-col>
      </v-container>
    </v-form>
</template>

<script>
export default {
    name: 'Creationprofil',
    data: function(){
    return {
      valid: false,

      name: '',
      budget: null,

      isNum: [
        v => !isNaN(v) || 'La valeur doit être un nombre.',
        v => !!v || 'Champ requis.',
        v => v > 0 || 'La valeur ne peut être négative.'
      ],
      isEmpty: [
        v => !!v || 'Champ requis.'
      ]
    };
  },
  methods: {
    submit() {
            if(this.$refs.form.validate()){
            localStorage.setItem('nom', this.name);
            localStorage.setItem('budget', this.budget);

            this.$router.push('budget');
            }
        }
    }
}
</script>