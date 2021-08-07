<template>
    <div>
        <contact-entry 
        v-for="(contact, index) in contacts" 
        :key="index" 
        :contact="contact" 
        @delete-entry="deleteEntry(contact)"
        @update-entry="updateEntry(contact)">
        </contact-entry>
        <add-new-entry 
        v-on:add-entry='addEntry'>
        </add-new-entry>
    </div>
</template>

<script>
import AddNewEntry from './AddNewEntry.vue'
import ContactEntry from './ContactEntry.vue'

export default {
    props:['contacts'],
    components:{
        AddNewEntry,
        ContactEntry,
    },
    methods:{
        deleteEntry(x){
            const index = this.contacts.indexOf(x)
            this.contacts.splice(index, 1)
            this.saveContacts()
        },
        addEntry(x){
            this.contacts.push(x)
            this.saveContacts()
        },
        updateEntry(x){
            const index = this.contacts.indexOf(x)
            this.contacts[index] = x
            this.saveContacts()
        },
        saveContacts(){
            const parsed = JSON.stringify(this.contacts)
            localStorage.setItem('contacts', parsed)
        }
    }
}
</script>

<style>

</style>