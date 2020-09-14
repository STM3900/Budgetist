<template>
  <h1 class="display-3 mt-16 mb-2">{{titre}} {{nom}} !</h1>
</template>

<script>
export default {
  name: "Test",
  props: ["titre", "nom"],
};
</script>
