<template>
  <div id="app">
    <contact-list v-bind:contacts="contacts"></contact-list>
  </div>
</template>

<script>
import ContactList from './components/ContactList.vue'

export default {
  name: 'App',
  components: {
    ContactList,
  },
  data(){
    return{
      contacts:[
        {
          first_name: 'Herp',
          last_name: 'Derp',
          number: '065-65505544',
          category: 'Work',
        },
        {
          first_name: 'Smor',
          last_name: 'Duur',
          number: '065-65505544',
          category: 'Home',
        },
        {
          first_name: 'Todo',
          last_name: 'Todoovic',
          number: '065-65505544',
          category: 'Work',
        },
        {
          first_name: 'Kek',
          last_name: 'Bur',
          number: '065-65505544',
          category: 'Home',
        },
      ]
    }
  },
  mounted(){
    if(localStorage.contacts){
      this.contacts = localStorage.contacts
    }
  },
  watch: {
    contacts(newContacts) {
      localStorage.contacts = newContacts
    }
  }
}
</script>

<style>
#app{
  margin-top: 50px;
}

</style>
