<template>
    <form @submit.prevent="submitForm">
        <div class="form-control">
            <label for="firstname">Firstname</label>
            <input type="text" id="firstname" v-model.trim="firstName">
        </div>
        <div class="form-control">
            <label for="lastname">Lastname</label>
            <input type="text" id="lastname" v-model.trim="lastName">
        </div>
        <div class="form-control">
            <label for="description">Description</label>
            <textarea rows="5" id="description" v-model.trim="description"></textarea>
        </div>

        <div class="form-control">
            <label for="rate">Hourly Rate</label>
            <input type="number" id="rate" v-model.number="rate">
        </div>

        <div class="form-control">
            <h3>Areas of Expertise</h3>
            <div>
                <input type="checkbox" name="" id="frontend" value="frontend" v-model="areas">
                <label for="frontend">Frontend Development</label>
            </div>
            <div>
                <input type="checkbox" name="" id="backendd" value="backend" v-model="areas">
                <label for="backend">Backend Development</label>
            </div>
            <div>
                <input type="checkbox" name="" id="career" value="career" v-model="areas">
                <label for="frontend">Career Advisory</label>
            </div>
        </div>

        <BaseButton >Register</BaseButton>
    </form>
</template>

<script>
export default{
    emits:['save-data'],
    data(){
        return{
            firstName: '',
            lastName: '',
            description: '',
            rate: null,
            areas: []
        }
    },
    methods:{
        submitForm(){
            const formData = {
                first: this.firstName,
                last: this.lastName,
                desc: this.description,
                rate: this.rate,
                areas: this.areas
            };

            this.$emit('save-data', formData)
        }
    }
}
</script>