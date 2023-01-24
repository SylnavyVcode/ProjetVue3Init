<template>
  <div>
    <!-- Modal trigger button -->

    <!-- Modal Body -->
    <!-- if you want to close by clicking outside the modal, delete the last endpoint:data-bs-backdrop and data-bs-keyboard -->
    <div
      class="modal fade"
      id="modalId"
      tabindex="-1"
      data-bs-backdrop="static"
      data-bs-keyboard="false"
      role="dialog"
      aria-labelledby="modalTitleId"
      aria-hidden="true"
    >
      <div
        class="modal-dialog modal-dialog-scrollable modal-dialog-centered modal-sm"
        role="document"
      >
        <div class="modal-content">
          <div class="modal-header">
            <h5 class="modal-title" id="modalTitleId">Modal title</h5>
            <button
              type="button"
              class="btn-close"
              data-bs-dismiss="modal"
              aria-label="Close"
            ></button>
          </div>
          <div class="modal-body">

            <div class="mb-3">
              <label for="" class="form-label">Email</label>
              <input type="email" class="form-control" v-model="person.email" name="" id="" aria-describedby="emailHelpId" placeholder="abc@mail.com">
              <small v-if="error.email" id="emailHelpId" class="form-text text-danger">Email Invalid</small>
            </div>
            <div class="mb-3">
              <label for="" class="form-label">Password</label>
              <input type="password" class="form-control" v-model="person.password" name="" id="" aria-describedby="emailHelpId" placeholder="**********">
              <small v-if="error.password" id="emailHelpId" class="form-text text-danger">Password Invalid</small>
            </div>

          </div>
          <div class="modal-footer">
            
            <button @click="login()" type="button" class="btn btn-primary">
              <i class="bi bi-person-circle"></i>
              Log In
            </button>
          </div>
        </div>
      </div>
    </div>

    <!-- Optional: Place to the bottom of scripts -->
 
  </div>
</template>
<script>
export default {
  data() {
    return {
      person : {
        email: '',
        password:''
      },
      error:{
        email:false,
        password:false,
      }
    }
  },
  methods: {
    login(){
      if(this.person.email.trim() === ''){
        this.error.email = true
        this.error.password = false
      }else{
        if(this.person.password.trim() === ''){
        this.error.password = true
        this.error.email = false
      }else{
        this.error.email = false
        this.error.password = false
      }
      }
    }
  },
};
</script>
<style></style>
