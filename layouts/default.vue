<template>
  <div>
    <v-app>
      <Nuxt />
    </v-app>
  </div>
</template>

<style>
.v-main{
  margin-right: auto;
  margin-left: auto;

  width: 900px;
}

html {
  font-family:
    'Source Sans Pro',
    -apple-system,
    BlinkMacSystemFont,
    'Segoe UI',
    Roboto,
    'Helvetica Neue',
    Arial,
    sans-serif;
  font-size: 16px;
  word-spacing: 1px;
  -ms-text-size-adjust: 100%;
  -webkit-text-size-adjust: 100%;
  -moz-osx-font-smoothing: grayscale;
  -webkit-font-smoothing: antialiased;
  box-sizing: border-box;
}


*,
*::before,
*::after {
  box-sizing: border-box;
  margin: 0;

  text-decoration: none;
}

.button--green {
  display: inline-block;
  border-radius: 4px;
  border: 1px solid #3b8070;
  color: #3b8070;
  text-decoration: none;
  padding: 10px 30px;

  transition: 0.3s;
  margin-top: 5px;
  margin-bottom: 5px;
}

.button--green:hover {
  color: #fff;
  background-color: #3b8070;
}

.button--grey {
  display: inline-block;
  border-radius: 4px;
  border: 1px solid #35495e;
  color: #35495e;
  text-decoration: none;
  padding: 10px 30px;
  margin-top: 5px;
  margin-bottom: 5px;

  transition: 0.3s;
}

.button--grey:hover {
  color: #fff;
  background-color: #35495e;
}

/*truc de transition*/

.fade-enter-active,
.fade-leave-active {
  transition-duration: 0.3s;
  transition-property: opacity;
  transition-timing-function: ease;
}

.fade-enter,
.fade-leave-active {
  opacity: 0;
} 
</style>
