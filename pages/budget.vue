<template>
  <v-main>
    <div v-resize="onResize" :class="`${margin}`">
      <Test v-bind:titre="letitre" v-bind:nom="nom"/>
        <v-row justify="space-between">
          <v-col cols="12" sm="6">
            <Budget v-bind:budget="budget" v-bind:devise="devise"/>
          </v-col>
          <v-col cols="12" sm="6">
            <Reste v-bind:reste="reste" v-bind:devise="devise" v-bind:couleur="couleur"/>
          </v-col>
        </v-row>
      <Nodepense v-if="!isDepense" v-on:submit="ajouterDepense" class=" mt-10 mb-10"/>
      <!-- <transition-group name="list-complete"> -->
        <Depense class="list-complete-item" v-for="depense in depenses" :key="depense.id" v-bind:numDepense="depense.id" v-bind:montantDepense="depense.montant" v-bind:texteDepense="depense.texte" v-bind:date="depense.date" v-bind:devise="devise" v-bind:icone="depense.type" v-on:suppr="supprimerDepense(depense.id)" />
      <!-- </transition-group> -->
      <v-container class="pl-0 pr-0">
        <v-row justify="space-between" align="start">
          <v-col cols="12" sm="4">
            <v-btn block outlined color="grey darken-1" v-on:click="$router.push('/');"><v-icon left>arrow_back</v-icon>Revenir au menu</v-btn>
          </v-col>
          <v-col cols="12" sm="4">
            <AjouterDepense v-if="isDepense" v-on:submit="ajouterDepense" :depressedState='false'/>
          </v-col>
        </v-row>
      </v-container>
    </div>
  </v-main>
</template>

<script>
const STORAGE_KEY = 'depenses-storage';

import Test from "../components/Test";
import Budget from "../components/Budget";
import Depense from "../components/Depense";
import Reste from "../components/Reste";

import AjouterDepense from "../components/AjouterDepense";
import Popup from "../components/Popup";
import Nodepense from "../components/Nodepense";

export default {
  transition: 'fade',
  components: {
    Test, Budget, Depense, Reste, AjouterDepense, Popup, Nodepense
  },
  data() {
    return {
      letitre: "Bonjour",
      nom: "",
      budget: null,
      devise: '€',

      couleur: 'indigo',
      isDepense: true,

      depenses: [
        
      ],
      reste: '',
      margin: ''
    }
  },
  methods: {
    test(){
      alert('test');
    },
    calculDepense(){
      this.checkDepense();
      this.reste = this.budget;

      if(this.depenses){
        for(let i = 0; i < this.depenses.length; i++){

        this.reste = this.reste - this.depenses[i].montant;
        this.depenses[i].id = i+1;
        }
      }
      this.calculCouleur();
    },
    ajouterDepense(data){
      this.depenses.push({id: '', montant: data.montant, texte: data.texte, date: new Date().toLocaleDateString(), type: data.type});

      this.calculDepense();
      localStorage.setItem(STORAGE_KEY, JSON.stringify(this.depenses));
    },
    supprimerDepense(index){
      this.depenses.splice(index-1, 1);

      this.calculDepense();
      localStorage.setItem(STORAGE_KEY, JSON.stringify(this.depenses));
    },
    calculCouleur(){
      if(this.reste >= this.budget*0.75){
        this.couleur = 'blue';
      }else if(this.reste >= this.budget*0.50){
        this.couleur = 'success';
      }else if(this.reste >= this.budget*0.25){
        this.couleur = 'amber';
      }else if(this.reste >= this.budget*0.10){
        this.couleur = 'warning';
      }else if(this.reste <= this.budget*0.10 && this.reste > 0){
        this.couleur = 'error';
      }else if(this.reste <= 0){
        this.couleur = 'pink';
      }
    },
    checkDepense(){
      if(this.depenses.length < 1){
        this.isDepense = false;
      }
      else{
        this.isDepense = true;
      }
    },
    onResize(){
      this.windowSize = { x: window.innerWidth, y: window.innerHeight };
      this.setPadding();
    },
    setPadding(){
      if(this.windowSize.x < 960){
        this.margin = 'ml-5 mr-5';
      }
      else{
        this.margin = '';
      }
    }
  },
  mounted() {
      if(localStorage.getItem("nom") == "" || localStorage.getItem("nom") == undefined){
        this.$router.push('/');
      }
      else{
        this.nom = localStorage.getItem("nom");
        this.budget =  localStorage.getItem("budget");

        this.depenses = JSON.parse(localStorage.getItem(STORAGE_KEY) || '[]');
        this.calculDepense();
      }
      this.onResize();
  },
};

</script>

<style>
.list-complete-item {
  transition: all .5s;
  width: 900px;
}
.list-complete-enter, .list-complete-leave-to{
  opacity: 0;
  transform: translateY(30px);
}
.list-complete-leave-active {
  position: absolute;
}
</style>
