<template>
    <div class="ui centered card">
        <div class='content'>
            <div class='header'>
                {{contact.first_name}} {{contact.last_name}}
                <span class='right floated icon'>
                    <i class='icon outline' :class="{building: contact.category == 'Work', home: contact.category == 'Home'}"></i>
                    <!-- Cisto da prikazemo dinamicko dodavanje klasa -->
                </span>
            </div> 
            <div class='meta'>
                {{ contact.number }}
            </div>
            <div class='extra content'>
                <span class='right floated edit icon' v-on:click="toggleForm()">
                    <i class='edit icon'></i>
                </span>
                <span class='right floated trash icon' v-on:click="deleteEntry(contact)">
                    <i class='trash icon'></i>
                </span>
            </div>
        </div>
        <!-- form for editing !-->
        <div class='content' v-show='isEditing'>
            <div class='ui form'>
                <div class='field'>
                    <label>First Name</label>
                    <input type='text' v-model="contact.first_name" >
                </div>
                <div class='field'>
                    <label>Last Name</label>
                    <input type='text' v-model="contact.last_name" >
                </div>
                <div class='ui two button attached buttons'>
                    <button class='ui basic blue button' v-on:click="toggleForm()">
                        Close X
                    </button>
                </div>
            </div>
        </div> <!-- end form !-->
    </div>
</template>

<script>
export default {
    props:['contact'],
    data(){
        return{
            isEditing: false,
        }
    },
    methods:{
        toggleForm(){
            this.isEditing = !this.isEditing
        },
        deleteEntry(contact){
            this.$emit('delete-entry', contact)
        },
    }
}
</script>