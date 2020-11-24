<template>
  <div id="container">
    <img class="icon-header" src="../../resources/icon.png">
    <h1>Capital Final</h1>
  </div>
</template>

<script lang="ts">

export default {
  name: 'Header',
  props: {
    name: String
  }
}
</script>

<style scoped>
.icon-header {
  height: 4rem;
}

h1 {
  margin-top: 0rem;
}

#container {
  text-align: center;
  position: absolute;
  left: 0;
  right: 0;
  top: 13%;
  transform: translateY(-50%);
}
</style>