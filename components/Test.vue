<template>
  <h1 class="display-3 mt-10">{{titre}} {{nom}} !</h1>
</template>

<script>
export default {
  name: "Test",
  props: ["titre", "nom"],
};
</script>
