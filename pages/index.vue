<template>
  <v-main>
    <v-img :src="require('@/assets/budget.jpg')"></v-img>
    <h1 class="display-2 text-center mt-5  blue--text text--darken-4">{{titre}}</h1>
    <v-form ref="form" v-if="firstTime" v-on:submit.prevent="submit" v-model="valid">
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
    <v-container v-else>
      <v-col align="center">
        <v-col sm="5">
          <nuxt-link to="budget"><v-btn color="info" block outlined><v-icon left>arrow_right_alt</v-icon>Aller au budget</v-btn></nuxt-link> 
        </v-col>
        <v-col sm="5">
          <v-btn color="warning" outlined block v-on:click="reset"><v-icon left>delete</v-icon>Réinitialiser votre profil</v-btn>
        </v-col>
      </v-col>
    </v-container>
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
      titre : 'Bienvenue sur Budgetist !',

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
        localStorage.clear();

        this.firstTime = true;
        this.name = '';
        this.budget = null;
        this.checkTitle();
      },
      checkTitle(){
        if(this.firstTime){
          this.titre = 'Bienvenue sur Budgetist !';
        }
        else{
          this.titre = `Ravi de vous revoir, ${this.name} !`;
        }
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
      this.checkTitle();
  },
};
</script>

<style>
  *{
    text-decoration: none;
  }
</style>