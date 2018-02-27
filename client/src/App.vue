<template>
  <div id="app">
    <Phonebook/>
  </div>
</template>

<script>
import Phonebook from './components/Phonebook';

export default {
  name: 'App',
  components: {
    Phonebook,
  },
};
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #50392c;
}
</style>
