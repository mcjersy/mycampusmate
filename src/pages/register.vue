<template>
  <p>{{ form }}</p>
  <div class="wrapper p-5" style="color: darkmagenta;">
    <div class="container">
      <form class="bg-white p-5 bg-blur" @submit.prevent="registerUser">
        <h1>User Registration</h1>
        <hr />
        <div class="row mb-3 gy-2">
          <div class="col-md-3">
            <label class="form-label">First Name</label>
            <input type="text" class="form-control" required v-model="form.first_name"/>
          </div>
          <div class="col-md-3">
            <label class="form-label">Middle Name</label>
            <input type="text" class="form-control" required v-model="form.middle_name"/>
          </div>
          <div class="col-md-3">
            <label class="form-label">Last Name</label>
            <input type="text" class="form-control" required v-model="form.last_name"/>
          </div>
          <div class="col-md-3">
            <label class="form-label">Name Extension</label>
            <input type="text" class="form-control" required v-model="form.name_extension"/>
          </div>
          <div class="col-md-6">
            <label class="form-label">Birthday</label>
            <input type="date" class="form-control" required v-model="form.birthday"/>
          </div>
          <div class="col-md-6">
            <label class="form-label">Sex</label>
            <select class="form-select" v-model="form.sex">
              <option selected value="" disabled>--Select--</option>
              <option value="Male">Male</option>
              <option value="Female">Female</option>
            </select>
          </div>
          <div class="col-12">
            <label class="form-label">Address</label>
            <input type="text" class="form-control" required v-model="form.adress"/>
          </div>
          <div class="col-md-6">
            <label class="form-label">Contact Number</label>
            <input type="text" class="form-control" required v-model="form.contact_number"/>
          </div>
          <div class="col-md-6">
            <label class="form-label">Emergency Contact Number</label>
            <input type="text" class="form-control" required v-model="form.emergency_contact_number"/>
          </div>
          <div class="col-md-6">
            <label class="form-label">Student ID Number</label>
            <input type="text" class="form-control" required v-model="form.student_id_number"/>
          </div>
          <div class="col-md-6">
            <label class="form-label">Picture of ID</label>
            <input class="form-control" type="file" required accept="image/*" @change= "fileselected"/>
          </div>
          <div class="col-md-6">
            <label class="form-label">Username</label>
            <input type="text" class="form-control" required v-model="form.username"/>
          </div>
          <div class="col-md-6">
            <label class="form-label">Email</label>
            <input type="email" class="form-control" required v-model="form.email"/>
          </div>
          <div class="col-12">
            <label class="form-label">Password</label>
            <input type="password" class="form-control" required v-model="form.password"/>
          </div>
          <div class="col-12">
            <div class="form-check">
              <input
                class="form-check-input"
                type="checkbox"
                :value="false"
                id="confirm"
                required
              />
              <label class="form-check-label fst-italic text-sm" for="confirm">
                In submitting this form I agree to my details being used for the
                website and I also understand that my data will be held
                securely. I understand that when this information is no longer
                required for this purpose my data will be disposed properly.
              </label>
            </div>
          </div>
        </div>

        <!-- SHOW ONLY THIS SUCCESS MESSAGE WHEN SUCCESSFULLY REGISTERED -->
        <!-- <div class="alert alert-success" role="alert" v-if="showSuccess">
          <span class="fw-bold">Successfully registered!</span> You will have to
          wait for the confirmation of your account from the admin before you
          can login.
        </div> -->

        <!-- SHOW ONLY THIS ERROR MESSAGE WHEN REGISTER FAILED -->
        <!-- <div class="alert alert-danger" role="alert" v-if="errorMsg">
          <span class="fw-bold">{{ errorMsg }}</span>
        </div> -->

        <button type="submit" class="btn btn-danger">Register</button>
        <a href="/login" class="btn btn-secondary ms-2">Back</a>
      </form>
    </div>
  </div>
</template>
<script setup>
import { ref } from "vue";
import api from "@/http/api";

const form = ref ({
  first_name: "",
  middle_name:"",
  last_name:"",
  name_extension:"",
  birthday:"",
  sex:"",
  adress:"",
  contact_number:"",
  emergency_contact_number:"",
  student_id_number:"",
  file:"",
  username:"",
  email:"",
  password:"",
  confirm:false,
  usertype: 2,
  is_aproved: 1,

});
const fileselected = (e) => {
  const input = e.target;
  if (!input.file || input.file.length === 0) return;

  form.value.file = input.files[0];
};

async function registerUser(){
  const result = await api.post("/jwt/register/",form.value,{
    headers: {"Content-Type":"multipart/form-data"},
  });
  console.log(result)


}

</script>
<style scoped>
.wrapper {
  background-color: black;
  min-height: 100vh;
}
.btn-danger{
  color:violet;
  background-color:black;
}
.text-sm {
  font-size: 0.8rem;
}
.btn-secondary{
  color:violet;
  background-color: black;
}
.btn-secondary:hover{
  background-color: blanchedalmond;
  color: black;
}
.btn-danger:hover{
  background-color: blanchedalmond;
  color: black;
}
p{
  font-family: Arial, Helvetica, sans-serif;
  color: violet;
  background-color: black;
  font-size:larger;
}
input{
  color:blueviolet;
}
</style>


