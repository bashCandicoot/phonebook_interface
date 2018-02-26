<template>
  <div class="hello">
    <h1>{{ header }}</h1>
    <div v-for="contact in contacts" v-bind:key="contact">
      <div>
        {{ contact.name }} <span>{{ contact.phone_number }}</span>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'Phonebook',
  data() {
    return {
      header: 'Phonebook',
      contacts: null
    };
  },
  created() {
    this.getContacts()
  },
  methods:{
    getContacts() {
      axios.get('http://www.mocky.io/v2/581335f71000004204abaf83')
      .then(response => {
        this.contacts = response.data.contacts;
        // this.createPhonebook(this.contacts)
      })
      .catch(error => {
        console.error(error);
      })
    },

  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
