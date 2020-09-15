<template>
  <v-main>
    <h1>Bienvenue sur Budgetist !</h1>
    <v-form ref="form" v-if="firstTime" v-on:submit.prevent="submit" v-model="valid">
      <v-text-field type="text" label="Entrez votre nom" v-model="name" :rules="isEmpty"></v-text-field>
      <v-text-field type="number" label="Entrez votre budget" v-model="budget" :rules="isNum"></v-text-field>
      <v-btn :disabled="!valid" type="submit" class="success">C'est parti !</v-btn>
    </v-form>
    <v-btn class="warning" v-on:click="reset">Reset</v-btn>
  </v-main>
</template>

<script>
export default {
  transition: 'fade',
  data: function(){
    return {
      valid: false,
      name: '',
      budget: null,

      firstTime: true,

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

          console.log(this.newType);
          this.$router.push('budget');
        }
      },
      reset(){
        localStorage.removeItem('nom');
        localStorage.removeItem('budget');

        this.firstTime = true;
        this.name = '';
        this.budget = null;
      }
  },
    mounted() {
      if(localStorage.getItem("nom") == "" || localStorage.getItem("nom") == undefined){
        this.firstTime = true;
      }
      else{
        this.firstTime = false;

        this.name = localStorage.getItem('nom')
        this.budget = localStorage.getItem('budget')
      }
  },
};
</script>

<style>
  *{
    text-decoration: none;
  }
</style>