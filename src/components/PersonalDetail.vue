<template>
  <div class="PersonalDetail">
     <!-- Personal Detail -->
     <div class="row my-5">
      <div class="col-12">
        <h5 class="mb-4"><b>Personal Detail</b></h5>
      </div>
      <div class="col-6">
        <div class="form-group">
          <label for="job">Wanted Job Title</label>
          <select name="job" v-model="form.job" class="form-control" id="job" :disabled="disabled_form">
            <option value="web_developer">Web Developer</option>
            <option value="android_developer">Android Developer</option>
          </select>
        </div>
      </div>
      <div class="col-6 d-flex align-items-center">
        <img v-if="imgs == null" class="mr-4" :src="require(`@/assets/profile.jpg`)" alt="" style="width:10%">
        <img v-else class="mr-4" :src="imgs" alt="" style="width:10%">

        <input type="file"  @change="changeImage" id="actual-btn" :disabled="disabled_form" hidden/>
        <label id="imgs" for="actual-btn"  class="label-upload text-primary">Upload Foto</label>
      </div>

       <div class="col-6">
          <div class="form-group">
            <label for="firstName">First Name</label>
            <input v-model="form.firstName" type="text" class="form-control" id="firstName" :disabled="disabled_form">
          </div>
        </div> 
        <div class="col-6">
          <div class="form-group">
            <label for="lastName">Last Name</label>
            <input v-model="form.lastName" type="text" class="form-control" id="lastName" :disabled="disabled_form">
          </div>
        </div> 
        <div class="col-6">
          <div class="form-group">
            <label for="email">Email</label>
            <input v-model="form.email" type="email" class="form-control" id="email" :disabled="disabled_form">
          </div>
        </div> 
        <div class="col-6">
          <div class="form-group">
            <label for="phone">Phone</label>
            <input v-model="form.phone" type="number" class="form-control" id="phone" :disabled="disabled_form">
          </div>
        </div> 
        <div class="col-6">
          <div class="form-group">
            <label for="country">Country</label>
            <select name="country" v-model="form.country" class="form-control" id="country" :disabled="disabled_form">
              <option value="Indonesia">Indonesia</option>
              <option value="Jepang">Jepang</option>
            </select>
          </div>
        </div> 
        <div class="col-6">
          <div class="form-group">
            <label for="city">City</label>
            <select name="city" v-model="form.city" class="form-control" id="city" :disabled="disabled_form">
              <option value="jakarta">Jakarta</option>
              <option value="bogor">Bogor</option>
            </select>
          </div>
        </div> 
        <div class="col-6">
          <div class="form-group">
            <label for="postalCode">Postal Code</label>
            <input v-model="form.postalCode" type="number" class="form-control" id="postalCode" :disabled="disabled_form">
          </div>
        </div> 
        <div class="col-6">
          <div class="form-group">
            <label for="drivingLicence">Driving Licence</label>
            <input v-model="form.drivingLicence" type="number" class="form-control" id="drivingLicence" :disabled="disabled_form">
          </div>
        </div> 
        <div class="col-6">
          <div class="form-group">
            <label for="Nationality">Nationality</label>
            <select name="nationality" v-model="form.nationality" class="form-control" id="nationality" :disabled="disabled_form">
              <option value="wni">WNI</option>
              <option value="wna">WNA</option>
            </select>
          </div>
        </div> 
        <div class="col-6">
          <div class="form-group">
            <label for="placeOfBirth">place birth</label>
            <input v-model="form.placeOfBirth" type="text" class="form-control" id="placeOfBirth" :disabled="disabled_form">
          </div>
        </div> 
        <div class="col-6">
          <div class="form-group">
            <label for="dateOfBirth">Date Of Birth</label>
            <input v-model="form.dateOfBirth" type="date" class="form-control" id="dateOfBirth" :disabled="disabled_form">
          </div>
        </div> 
        <div class="col-12 d-flex flex-row-reverse my-4">
          <button v-if="disabled_form" class="btn btn-warning" @click.prevent="disabled_form = false">Edit</button>
          <button v-else class="btn btn-primary" @click.prevent="submit">Save</button>
        </div>
     </div>
  </div>
</template>
<script>
import $ from "jquery";

export default {
  data() {
    return{
      imgs: null,
      datas : {},
      form : {},
      disabled_form: false
    }
  },
  methods:{
    changeImage(e){
      const file = e.target.files[0];
      this.form.img = e.target.files[0]
      this.imgs = URL.createObjectURL(file);
    },

    submit(){
        let job = $('select[name=job]').val()
        let firstName = $('#firstName').val();
        let lastName = $('#lastName').val();
        let email = $('#email').val();
        let phone = $('#phone').val();
        let country = $('#country').val();
        let city = $('select[name=city]').val()
        let postalCode = $('#postalCode').val();
        let drivingLicence = $('#drivingLicence').val();
        let nationality = $('select[name=nationality]').val()
        let placeOfBirth = $('#placeOfBirth').val();
        let dateOfBirth = $('#dateOfBirth').val();
        
        $(".error").remove();
       
        if (job == null) {
          $('#job').after('<span class="error text-danger">This field is required</span>');
        }
        if (country == null) {
          $('#country').after('<span class="error text-danger">This field is required </span>');
        }
        if (dateOfBirth == '') {
          $('#dateOfBirth').after('<span class="error text-danger">This field is required</span>');
        }
        if (nationality == null) {
          $('#nationality').after('<span class="error text-danger">This field is required</span>');
        }
        if (city ==  null) {
          $('#city').after('<span class="error text-danger">This field is required</span>');
        }
        if (firstName.length < 1 || firstName.length > 50) {
          $('#firstName').after('<span class="error text-danger">This field is required, and max 50 character</span>');
        }
        if (placeOfBirth.length < 1 || placeOfBirth.length > 50) {
          $('#placeOfBirth').after('<span class="error text-danger">This field is required, and max 50 character</span>');
        }
        if (lastName.length < 1 || lastName.length > 50) {
          $('#lastName').after('<span class="error text-danger">This field is required, and max 50 character</span>');
        }
        if (email.length < 1 || email.length > 50) {
          $('#email').after('<span class="error text-danger">This field is required, and max 50 character</span>');
        }
        if (phone.length < 1 || phone.length > 50) {
          $('#phone').after('<span class="error text-danger">This field is required, and max 50 character</span>');
        }
        if (postalCode.length < 1 || postalCode.length > 50) {
          $('#postalCode').after('<span class="error text-danger">This field is required, and max 50 character</span>');
        }
        if (drivingLicence.length < 1 || drivingLicence.length > 50) {
          $('#drivingLicence').after('<span class="error text-danger">This field is required, and max 50 character</span>');
        }

        if($(".error").length > 0) {
          $('html, body').animate({
            scrollTop: 0
          }, 1000); 
        }else{
          this.$emit("datas", this.form)
          this.disabled_form = true
        }
    },
   
  },


}
</script>

<style>
/* input, select, textarea{
    background-color: #f3f3f3 !important;
} */

label {
  color : rgb(117, 115, 115);
}
</style>