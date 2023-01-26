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
        class="modal-dialog modal-dialog-scrollable modal-dialog-centered modal-md"
        role="document"
      >
        <div class="modal-content p-2">
          <div class="modal-header">
            <h5 v-if="state" class="modal-title" id="modalTitleId">Log In</h5>
            <h5 v-else class="modal-title" id="modalTitleId">Sign Up</h5>
            <button ref="btnClose"
              type="button"
              class="btn-close"
              data-bs-dismiss="modal"
              aria-label="Close"
            ></button>

          </div>
          <div class="modal-body">
            <div class="mb-3">
              <label for="" class="form-label">Email</label>
              <input
                type="email"
                class="form-control"
                v-model="person.email"
                name=""
                id=""
                aria-describedby="emailHelpId"
                placeholder="abc@mail.com"
              />
              <small
                v-if="error.email"
                id="emailHelpId"
                class="form-text text-danger"
                >Email Invalid</small
              >
            </div>
            <div class="mb-3">
              <label for="" class="form-label">Password</label>
              <input
                type="password"
                class="form-control"
                v-model="person.password"
                name=""
                id=""
                aria-describedby="emailHelpId"
                placeholder="**********"
              />
              <small
                v-if="error.password"
                id="emailHelpId"
                class="form-text text-danger"
                >Password Invalid</small
              >
            </div>
            <div v-if="!state" class="mb-3">
              <label for="" class="form-label"> Confirm password</label>
              <input
                type="password"
                class="form-control"
                v-model="person.confPassword"
                name=""
                id=""
                aria-describedby="emailHelpId"
                placeholder="**********"
              />
              <small
                v-if="error.confPassword"
                id="emailHelpId"
                class="form-text text-danger"
                >Confirm password Invalid</small
              >
            </div>
            <div class="row mb-3">
              <div class="mx-3 col-6 form-check">
                <input
                  class="form-check-input"
                  type="checkbox"
                  value=""
                  id=""
                  checked
                />
                <label class="form-check-label" for="">
                  Se souvenir de moi.
                </label>
              </div>
              <div v-if="state" class="col text-end">
                <a href="" class="text-decoration-none">Forget password</a>
              </div>
            </div>
            <div v-if="state" class="row mt-4 text-center">
              <p>
                If you haven't a count please
                <span
                  @click="clickToSignUp()"
                  class="text-decoration-none text-primary"
                  style="cursor: pointer"
                  >Sign Up</span
                >.
              </p>
            </div>
            <div v-else class="row mt-4 text-center">
              <p>
                You have already a count please
                <span
                  @click="clickToLogIn()"
                  class="text-decoration-none text-primary"
                  style="cursor: pointer"
                  >Log In</span
                >.
              </p>
            </div>
          </div>
          <div class="modal-footer">
            <button
              v-if="state"
              @click="login()"
              type="button"
              class="btn btn-primary vw-100"
            >
              <i class="bi bi-person-circle"></i>
              Log In
            </button>
            <button
              v-else
              @click="signUp()"
              type="button"
              class="btn btn-primary vw-100"
            >
              <i class="bi bi-person-circle"></i>
              Sign Up
            </button>
          </div>
        </div>
      </div>

    </div>

    <!-- Optional: Place to the bottom of scripts -->
  </div>
</template>
<script>

import db from '@/data/user.json'

export default {
  data() {
    return {
      db:db,
      person: {
        email: "",
        password: "",
        confPassword: "",
      },
      error: {
        email: false,
        password: false,
        confPassword: false
      },
      state: true,
    };
  },
  methods: {
    signUp() {
      if (this.person.email.trim() === "") {
        this.error.email = true;
        this.error.password = false;
        this.error.confPassword = false;
      } else {
        if (this.person.password.trim() === "") {
          this.error.password = true;
          this.error.email = false;
          this.error.confPassword = false;
        } else {
          if (this.person.confPassword.trim() === "") {
            this.error.confPassword = true;
            this.error.email = false;
            this.error.password = false;
      }else{
          this.error.email = false;
          this.error.password = false;
          this.error.confPassword = false;
          
          if(this.person.confPassword != this.person.password){
            this.error.confPassword = true
  
          }else{
            this.error.confPassword = false
          }

      }  
        }
      }
    },
    login() {
      if (this.person.email.trim() === "") {
        this.error.email = true;
        this.error.password = false;
      } else {
        if (this.person.password.trim() === "") {
          this.error.password = true;
          this.error.email = false;
        } else {
          this.error.email = false;
          this.error.password = false;

          // Db
          console.log("mange");

         const response =  this.db.users.find(element => {
            return element.email == this.person.email && element.password == this.person.password
          });
          if(response){
            
            this.db.account = []

            this.db.account.push(response)

            this.$refs.btnClose.click()

            this.$emit('loginEmit')

          }
         
         
        }
      }
    },
    clickToSignUp() {
      this.state = false;
    },
    clickToLogIn() {
      this.state = true;
    },
  },
};
</script>
<style></style>
