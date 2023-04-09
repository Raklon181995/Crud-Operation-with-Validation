<template>
<div>
    <div class="container  mt-3">
        <div class="row">
            <div class="col">
                <p class="h3 text-danger fw-bold">Edit User</p>
            </div>
        </div>
    </div>
    <div class="container" mt-3>
        <div class="row">
            <div class="col-md-4">
               <form @submit.prevent="updateSubmit()">
                    <div class="mb-2">
                        <input required v-model="contact.name" type="text" class="form-control" placeholder="Name">
                    </div>
                    <div class="mb-2">Select Gender
                        <div class="d-flex">
                            <div class="form-check">
                                <input type="radio" v-model="contact.gender" value="male">&nbsp; Male
                                &nbsp;&nbsp;&nbsp;
                                <input type="radio" v-model="contact.gender" value="female">&nbsp; Female    
                            </div>
                        </div>
                    </div>
                    
                     <div class="mb-2">
                        <div>Select Skills</div>
                        <div class="ml-6" v-for="(skill, index) in skills" :key="index">
                            <input v-model="contact.skill" class="form-check-input" type="checkbox" :id="skill.text" :value="skill.text">
                            <label class="form-check-label ml-2" for="flexCheckDefault">
                                {{skill.text}}
                            </label>
                        </div>
                    </div>
                
                    <div class="mb-2">
                        <input required v-model="contact.photo" type="text" class="form-control" placeholder="Image">
                    </div>
                    <div class="mb-2">
                        <input required v-model="contact.mobile" type="number" class="form-control" placeholder="Phone">
                    </div>
                     <div class="mb-2">
                        <input required v-model="contact.country" type="text" class="form-control" placeholder="Country Name">
                    </div>
                    <div class="mb-2">
                        <input required type="submit" class="btn btn-success" value="Update">
                    </div>
               </form>
            </div>
            <div class="col-md-4">
                <img :src="contact.photo" alt="user image" class="user-img">
            </div>
        </div>
    </div>
</div>
</template>

<script>
import {ContactService} from "@/services/ContactService";
export default {
  name: 'EditDetails',
  data: function(){
    return{
    contactId: this.$route.params.contactId,
    loading: false,
    contact: {
        name: '',
        photo: '',
        country: '',
        mobile: '',
        gender: '',
        skill: '',
    },
    errorMessage: null
  }
 },
 created :async function() {
    try{
        this.loading = true;
        let response = await ContactService.getContact(this.contactId);
        this.contact = response.data;
        this.loading = false;

    }
    catch(error){
        this.errorMessage = error;
        this.loading = false;

    }
 },
 methods: {
    updateSubmit: async function() {
        try{
            let response =await ContactService.updateContact(this.contact, this.contactId);
            if(response){
                return this.$router.push('/');

            }
            else{
                return this.$router.push('/edit/${this.contactId}');
            }
        }
        catch(error){
            console.log(error);
        }
    }
 }
}
</script>