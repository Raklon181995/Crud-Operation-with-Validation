<template>
  <div>
    <div class="container  mt-3">
        <div class="row">
            <div class="col">
                <p class="h3 text-danger fw-bold">View User</p>
            </div>
        </div>
    </div>

    <div v-if="loading">
      <div class="container">
        <div class="row">
          <div class="col">
            <Loader />
          </div>
        </div>
      </div>
    </div>

    <div v-if="!loading && errorMessage">
      <div class="container">
        <div class="row">
          <div class="col">
          <p class="h3 text-danger fw-bold">{{errorMessage}}</p>
          </div>
        </div>
      </div>
    </div>
     <div class="container mt-3" v-if="!loading && isDone()">
        <div class="row">
            <div class="col-md-4 my-2 align-item-center" align="center">
                 <img :src="contact.photo" alt="user img" class="user-img" />
            </div>
            <div class="col-md-6">
                 <ul class="list-group">
                  <li class="list-group-item">Name: <span class="fw-bold">{{contact.name}}</span></li>
                  <li class="list-group-item">Phone: <span class="fw-bold">{{contact.mobile}}</span></li>
                   <li class="list-group-item">Gender: <span class="fw-bold">{{contact.gender}}</span></li>
                   <li class="list-group-item">Skills: <span class="fw-bold">{{contact.skill}}</span></li>
                  <li class="list-group-item">Country Name: <span class="fw-bold">{{contact.country}}</span></li>
                </ul>
            </div>
        </div>
        <div>
          <router-link to="/" class="btn btn-success my-2">Back</router-link>
        </div>
    </div>
  </div>
</template>

<script>
import {ContactService} from "@/services/ContactService";
import Loader from "../components/Loader";
export default {
  name: 'ViewDetails',
  components: {
   Loader
   },

 data: function() {
  return{
    contactId: this.$route.params.contactId,
    loading: false,
    contact: {},
 
  }
 },
 created: async function() {
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
  isDone: function() {
    return Object.keys(this.contact).length > 0;
  }
}
}
</script>