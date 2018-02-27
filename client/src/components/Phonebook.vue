<template>
  <div>
    <h1>{{ header }}</h1>
    <input type="text" name="search" v-model="search" placeholder="Search name/number..." class='search'>
    <button class="sort-button" @click="sortContactsByLastName">SORT</button>
    <div class="border"></div>
    <div class="contact" v-for="contact in filteredContacts" v-bind:key="contact.phone_number">
      <div @click="showAddress(contact)">
        <div class="name">{{ contact.name }}</div>
        <div class="phone-number">{{ contact.phone_number }}</div>
        <div class="address" v-if="selected === contact.phone_number">
          {{ contact.address }}
        </div>
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
      contacts: null,
      selected: null,
      search: null,
      sortDirection: '<'
    };
  },
  created() {
    this.getContacts()
  },
  computed: {
    filteredContacts() {
      if (!this.search) {
        return this.contacts;
      }
      return this.filterContactsByName();
    },
  },
  methods:{
    getContacts() {
      axios.get('http://www.mocky.io/v2/581335f71000004204abaf83')
      .then(response => {
        this.contacts = response.data.contacts;
      })
      .catch(error => {
        console.error(error);
      })
    },
    showAddress(contact) {
      this.selected = contact.phone_number;
    },
    filterContactsByName() {
      return this.contacts.filter((contact) => {
        const name = contact.name.toLowerCase();
        const number = contact.phone_number;
        const search = this.search.toLowerCase();
        return name.includes(search) || number.includes(search);
      });
    },
    sortContactsByLastName() {
      if (this.sortDirection === '<') {
        this.contacts.sort((a, b) => a.name.split(' ')[1] > b.name.split(' ')[1]);
        this.sortDirection = '>';
      } else {
        this.contacts.sort((a, b) => a.name.split(' ')[1] < b.name.split(' ')[1]);
        this.sortDirection = '<';
      }
    }
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

h1 {
  font-weight: bold;
  color: #bd8564;
  height: 100px;
  padding: 30px 20px 20px 20px;
  background-color: #50392c;
}

.border {
  border-bottom: 3px double #8c8b8b;
  padding: 2em;
}

.sort-button {
  border: none;
  display: block;
  text-align: center;
  cursor: pointer;
  position: relative;
  color: #bd8564;
  font-weight: 700;
  font-size: 15px;
  background-color: #50392c;
  padding: 9px 60px;
  margin: 0 auto;
  box-shadow: 0 5px 15px rgba(0,0,0,0.20);
}

.search {
  text-align: center;
  padding: 20px 20px 20px 20px;
  font-size: 20px;
}

.contact {
  padding: 2em;
  cursor: pointer;
  border-bottom: 3px double #8c8b8b;
}

.contact:hover {
  color: #bd8564;
}

.name {
  font-size: 20px;
}

.phone-number {
  opacity: 0.6;
}

.address {
  opacity: 0.6;
  font-size: 14px;
}

</style>
