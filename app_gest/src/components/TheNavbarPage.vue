<template>
  <main>
    <!-- ========== Start panier ========== -->

    <!-- Modal Body -->
    <!-- if you want to close by clicking outside the modal, delete the last endpoint:data-bs-backdrop and data-bs-keyboard -->
    <div
      class="modal fade"
      id="modalIdPanier"
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
        <div class="modal-content">
          <div class="modal-header">
            <h5 class="modal-title" id="modalTitleId">
              Mon panier
              <span class="badge rounded-pill text-bg-primary">{{
                somme()
              }}</span>
            </h5>
            <button
              type="button"
              class="btn-close"
              data-bs-dismiss="modal"
              aria-label="Close"
            ></button>
          </div>
          <div class="modal-body">
            <div class="table-responsive">
              <table class="table table-primary text-center">
                <thead>
                  <tr>
                    <th scope="col">Libellé</th>
                    <th scope="col">Prix</th>
                  </tr>
                </thead>
                <tbody>
                  <tr v-for="(item, id) in panier" :key="id" class="">
                    <td scope="row">{{ item.libelle }}</td>
                    <td>{{ item.price }}</td>
                  </tr>
                </tbody>
              </table>
            </div>
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
      <a
        class="nav-link text-dark"
        href="#"
        data-bs-toggle="modal"
        data-bs-target="#modalIdPanier"
      >
        <i class="bi bi-cart"></i>
        Panier
        <span class="badge rounded-pill text-bg-primary">
          {{ count }}
        </span>
      </a>
      <a
        v-if="db.account.at(0).email===''"
        class="nav-link text-dark"
        href="#"
        data-bs-toggle="modal"
        data-bs-target="#modalId"
      >
        <i class="bi bi-person"></i>
        {{ users.libelle }}
      </a>
      <a v-else @click="logOut()" class="nav-link text-dark" href="#">
        <i class="bi bi-person"></i>
        {{ users.libelle }}
      </a>
    </nav>
  </main>
</template>
<script>
import TheLoginPage from "../components/TheLoginPage.vue";
import db from "@/data/user.json";
export default {
  props: ["count"],
  components: { TheLoginPage },
  data() {
    return {
      users: {
        libelle: "Log out",
      },
      panier: [],
      db: db,
      state: true,
    };
  },
  methods: {
    logOut() {
     const d ={email: "", password:"", admin:false}
     this.db.account=[]
     this.db.account.push(d)
    },
    somme() {
      let sum = 0;
      this.panier.forEach((element) => {
        sum += element.price;
      });
      return sum;
    },

    setLogin() {
      this.$emit("loginIn");
    },
    getPanier() {
      setInterval(() => {
        // console.log(this.db.account.at(0));
        this.panier = this.db.card;
      }, 1000);
    },
    isConnect() {
      setInterval(() => {
        // console.log(this.db.account.at(0));
        if (this.db.account.at(0).email == "") {
          this.users.libelle = "Log In";
        } else {
          this.users.libelle = "Log Out";
        }
      }, 1000);
    },
  },
  mounted() {
    this.getPanier();
    this.isConnect();
  },
};
</script>
<style></style>
