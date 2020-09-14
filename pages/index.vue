<template>
  <v-content>
    <Test v-bind:titre="letitre" v-bind:nom="nom"/>
    <v-row>
      <v-col>
        <Budget v-bind:budget="budget" v-bind:devise="devise"/>
      </v-col>
      <v-col>
        <Reste v-bind:reste="reste" v-bind:devise="devise" v-bind:couleur="couleur"/>
      </v-col>
    </v-row>
    <v-alert type="info" v-if="!isDepense" class=" mt-10 mb-10">Pas de dépenses ! Ajoutez en une ci-dessous</v-alert>
    <Depense v-for="depense in depenses" :key="depense.id" v-bind:numDepense="depense.id" v-bind:montantDepense="depense.montant" v-bind:texteDepense="depense.texte" v-bind:date="depense.date" v-bind:devise="devise" v-bind:icone="depense.type" v-on:suppr="supprimerDepense(depense.id)" />
    <v-container class="pl-0 pr-0">
      <AjouterDepense v-on:submit="ajouterDepense" />
    </v-container>
  </v-content>
</template>

<script>
const STORAGE_KEY = 'depenses-storage';

import Test from "../components/Test";
import Budget from "../components/Budget";
import Depense from "../components/Depense";
import Reste from "../components/Reste";

import AjouterDepense from "../components/AjouterDepense";

export default {
  transition: 'fade',
  components: {
    Test, Budget, Depense, Reste, AjouterDepense
  },
  data() {
    return {
      letitre: "Bonjour",
      nom: "Théo",
      budget: 400,
      devise: '€',

      couleur: 'indigo',
      isDepense: true,

      depenses: [
      ],
      reste: ''
    }
  },
  methods: {
    test(){
      alert('test');
    },
    calculDepense(){
      this.checkDepense();
      this.reste = this.budget;

      if(!this.depenses){
        console.log('Pas de dépenses, pas de calcul');
      }
      else{
        for(let i = 0; i < this.depenses.length; i++){
        console.log(this.depenses[i].montant);

        this.reste = this.reste - this.depenses[i].montant;
        this.depenses[i].id = i+1;
        console.log(this.depenses[i].id);
        }
      }
      this.calculCouleur();
    },
    ajouterDepense(newMontantC, newTexteC, newType){
      this.depenses.push({id: '', montant: newMontantC, texte: newTexteC, date: new Date().toLocaleDateString(), type: newType});

      console.log('Élément ajouté !');
      this.calculDepense();
      localStorage.setItem(STORAGE_KEY, JSON.stringify(this.depenses));
    },
    supprimerDepense(index){
      this.depenses.splice(index-1, 1);

      console.log(`Élément n°${index} supprimé !`);
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
      console.log("la dépense est ", this.isDepense);
    }
  },
  mounted() {
    this.depenses = JSON.parse(localStorage.getItem(STORAGE_KEY) || '[]');
    console.log(this.depenses);
    this.calculDepense();
  },
};

</script>

<style>
.v-content{
  margin-right: auto;
  margin-left: auto;

  width: 900px;
}

.title {
  font-family: "Quicksand", "Source Sans Pro", -apple-system, BlinkMacSystemFont,
    "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}
</style>
