<template>
    <div>
        <contact-entry v-for="(contact, index) in contacts" :key="index" :contact="contact" @delete-entry="deleteEntry(contact)"></contact-entry>
        <add-new-entry v-on:add-entry='addEntry'></add-new-entry>
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
        deleteEntry(entry){
            const contactIndex = this.contacts.indexOf(entry)
            this.contacts.splice(contactIndex, 1)
        },
        addEntry(entry){
            this.contacts.push(entry)
        },
    }
}
</script>

<style>

</style>