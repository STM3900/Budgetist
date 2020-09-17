<template>
  <v-main>
    <v-img :src="require('@/assets/budget.jpg')"></v-img>
    <h1 class="display-2 text-center mt-5  blue--text text--darken-4">{{titre}}</h1>
    <v-fade-transition leave-absolute>
      <Creationprofil v-if="firstTime" />
      <Buttons v-else v-on:reset="reset" />
    </v-fade-transition>
  </v-main>
</template>

<script>
import Creationprofil from "../components/Creationprofil";
import Buttons from "../components/Buttons";

export default {
 components: {
    Creationprofil,Buttons
  },
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