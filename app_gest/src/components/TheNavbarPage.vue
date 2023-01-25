<template>
  <main>

    <!-- ========== Start panier ========== -->
    
      
      <!-- Modal Body -->
      <!-- if you want to close by clicking outside the modal, delete the last endpoint:data-bs-backdrop and data-bs-keyboard -->
      <div class="modal fade" id="modalIdPanier" tabindex="-1" data-bs-backdrop="static" data-bs-keyboard="false" role="dialog" aria-labelledby="modalTitleId" aria-hidden="true">
        <div class="modal-dialog modal-dialog-scrollable modal-dialog-centered modal-sm" role="document">
          <div class="modal-content">
            <div class="modal-header">
              <h5 class="modal-title" id="modalTitleId"> Card </h5>
                <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
            </div>
            <div class="modal-body">
              
              {{ card }}

            </div>

          </div>
        </div>
      </div>
      
    

    <!-- ========== End panier ========== -->

    <TheLoginPage @loginEmit="setLogin()"></TheLoginPage>

    <nav class="nav justify-content-center shadow p-2">
      <a class="nav-link active text-dark" href="#" aria-current="page">
        <i class="bi bi-boxes"></i>
        Products
      </a>
      <a class="nav-link text-dark" href="#" data-bs-toggle="modal" data-bs-target="#modalIdPanier">
        <i class="bi bi-cart"></i>
        Panier
        <span class="badge rounded-pill text-bg-primary">
          {{ count }}
        </span>
      </a>
      <a
        class="nav-link text-dark"
        href="#"
        data-bs-toggle="modal"
        data-bs-target="#modalId"
      >
        <i class="bi bi-person"></i>
        Log In
      </a>
    </nav>
  </main>
</template>
<script>
import TheLoginPage from "../components/TheLoginPage.vue";
export default {
  props: ["count"],
  components: {TheLoginPage},
  data() {
    return {
      panier:[]
    };
  },
  methods: {
    setLogin(){
      this.$emit('loginIn')
    },
    stateAccount(){

      setInterval(() => {
        //console.log(this.db.account.at(0));
        this.panier= this.db.account.card
      }, 100);

    },
  },
  mounted(){

    this.stateAccount();

  }
};
</script>
<style></style>
