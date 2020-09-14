<template>
  <div id="app-5">
    <p>{{ message }}</p>
    <button v-on:click="reverseMessage">Reverse Message</button> <br>
    <v-btn class="info">Message super cool</v-btn>
  </div>
</template>

<script>
export default {
  transition: 'fade',
  data() {
    return {
      message: "coucou",
    };
  },
  methods: {
    reverseMessage: function () {
      this.message = this.message.split("").reverse().join("");
    },
  },
};
</script>