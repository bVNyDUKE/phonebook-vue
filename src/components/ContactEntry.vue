<template>
    <div class="ui centered card">
        <div class='content'>
            <div class='header'>
                {{contact.first_name}} {{contact.last_name}}
                <span class='right floated icon'>
                    <i class='icon outline' :class="{building: contact.category == 'Work', home: contact.category == 'Home'}"></i>
                </span>
            </div> 
            <div class='meta'>
                {{ contact.number }}
            </div>
            <!-- <div class='extra content'>
                <span class='right floated edit icon' v-on:click="toggleForm(contact)">
                    <i class='edit icon'></i>
                </span>
                <span class='right floated trash icon' v-on:click="deleteEntry(contact)">
                    <i class='trash icon'></i>
                </span>
            </div> -->
            <div class='extra content'>
            <div class="ui small basic icon buttons attached">
                <button class="ui basic button" @click="toggleForm(contact)">
                    <i class="edit icon"></i>
                </button>
                <button class="ui basic button" @click="deleteEntry(contact)">
                    <i class="trash icon"></i>
                </button>
            </div>
            </div>
        </div>
        <!-- form for editing !-->
        <div class='content' v-show='isEditing'>
            <div class='ui form'>
                <div class='field' :class="{error: this.error.indexOf('firstName') != -1}">
                    <label>First Name</label>
                    <input type='text' v-model="contact.first_name" @input='validateForm'>
                </div>
                <div class='field' :class="{error: this.error.indexOf('lastName') != -1}">
                    <label>Last Name</label>
                    <input type='text' v-model="contact.last_name" @input='validateForm'>
                </div>
                <div class='field' :class="{error: this.error.indexOf('number') != -1}">
                    <label>Phone Number</label>
                    <input type='text' v-model="contact.number" @input='validateForm'>
                </div>
                <div class='ui attached buttons'>
                    <button class='ui green button' v-on:click="updateEntry(contact)">
                        Save
                    </button>
                    <button class='ui red button' v-on:click="cancelEdit(contact)">
                        Cancel
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
            cached : {},
            error: [],
            isEditing: false,
        }
    },
    methods:{
        validateForm(){
            this.error = []
            
            let nameRe = /^[a-zA-Z ]*$/
            let numberRe = /^[0-9 \- ]*$/

            if(this.contact.first_name.length >0 && !nameRe.test(this.contact.first_name)){
                this.error.push('firstName')
            }

            if(this.contact.last_name.length > 0 && !nameRe.test(this.contact.last_name)){
                this.error.push('lastName')
            }

            if(this.contact.number.length > 0 && !numberRe.test(this.contact.number)){
                this.error.push('number')
            }

            if(this.error.length != 0){
                return false
            }
            this.error = []
            return true
        },
        deleteEntry(x){
            this.$emit('delete-entry', x)
        },
        updateEntry(x){
            if(this.error.lengh != 0){
                return false
            }
            this.$emit('update-entry', x)
            this.toggleForm()
        },
        cancelEdit(x){
            Object.assign(x, this.cached)
            this.isEditing = !this.isEditing
            this.error = []
        },
        toggleForm(x){
            this.cached = Object.assign({}, x)
            this.isEditing = !this.isEditing
        },
    }
}
</script>