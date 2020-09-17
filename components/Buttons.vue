<template>
     <v-container>
      <v-col align="center">
        <v-col sm="5">
          <nuxt-link to="budget"><v-btn color="info" block outlined><v-icon left>arrow_right_alt</v-icon>Aller au budget</v-btn></nuxt-link> 
        </v-col>
        <v-col sm="5">
          <v-btn color="warning" outlined block v-on:click="$emit('reset');"><v-icon left>delete</v-icon>Réinitialiser votre profil</v-btn>
        </v-col>
      </v-col>
    </v-container>
</template>

<script>
export default {
    name: 'Buttons'
}
</script>