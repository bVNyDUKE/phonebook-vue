<template>
    <div class='ui basic content center aligned segment'>
        <button class='ui basic button icon' v-on:click="toggleForm">
            <i v-show='!isCreating' class='plus icon'></i>
            <i v-show='isCreating' class='minus icon'></i>
        </button>
        <div class='ui centered card' v-show="isCreating">
            <div class='content'>
                <div class='ui form'>
                    <div class='field' :class="{error: this.error.indexOf('firstName') != -1}" >
                        <label>First Name</label>
                        <input type='text' v-model="firstName" @change="validateForm">
                    </div>
                    <div class='field' :class="{error: this.error.indexOf('lastName') != -1}">
                        <label>Last Name</label>
                        <input type='text' v-model="lastName" @change="validateForm" >
                    </div>
                    <div class='field' :class="{error: this.error.indexOf('number') != -1}">
                        <label>Phone Number</label>
                        <input type='text' v-model="number" @change="validateForm" >
                    </div>
                    <div class='inline fields'>
                            <div class="ui radio checkbox">
                                <input type='radio' name='category' value='Home' checked='checked' v-model="category">
                                <label>Home <i class="home icon"></i></label>
                            </div>
                            <div class="ui radio checkbox">
                                <input type='radio' name='category' value='Work' v-model="category">
                                <label>Work <i class="building icon"></i></label>
                            </div>
                    </div>
                    <div class='ui buttons'>
                        <button class='ui blue button' v-on:click="sendForm">
                            Create
                        </button>
                        <button class='ui red button' v-on:click="toggleForm">
                            Cancel
                        </button>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    data(){
        return{
            firstName: '',
            lastName: '',
            number: '',
            category: 0,
            isCreating: false,
            error: [],
        }
    },
    methods:{
        toggleForm(){
            this.isCreating = !this.isCreating
        },
        validateForm(){
            this.error = []
            
            let nameRe = /^[a-zA-Z ]*$/
            let numberRe = /^[0-9 \- ]*$/

            if(this.firstName.length >0 && !nameRe.test(this.firstName)){
                this.error.push('firstName')
            }

            if(this.lastName.length > 0 && !nameRe.test(this.lastName)){
                this.error.push('lastName')
            }

            if(this.number.length > 0 && !numberRe.test(this.number)){
                this.error.push('number')
            }

            if(this.error.length != 0){
                return false
            }
            this.error = []
            return true
        },
        sendForm(){
                if (this.error.length == 0){
                const first_name = this.firstName
                const last_name = this.lastName
                const category = this.category
                const number = this.number
                this.$emit('add-entry',{
                    first_name,
                    last_name,
                    number,
                    category,
                })
                this.firstName = ''
                this.lastName = ''
                }
                this.toggleForm()
            }
           
        }
    }
</script>