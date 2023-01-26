<template>
  <div>
    <!-- ========== Start add product ========== -->

    <!-- Modal Body -->
    <!-- if you want to close by clicking outside the modal, delete the last endpoint:data-bs-backdrop and data-bs-keyboard -->
    <div
      class="modal fade"
      id="modalIdProduct"
      tabindex="-1"
      data-bs-backdrop="static"
      data-bs-keyboard="false"
      role="dialog"
      aria-labelledby="modalTitleId"
      aria-hidden="true"
    >
      <div
        class="modal-dialog modal-dialog-scrollable modal-dialog-centered modal-lg"
        role="document"
      >
        <div class="modal-content">
          <div class="modal-header">
            <h5 class="modal-title" id="modalTitleId">product</h5>
            <button
              type="button"
              class="btn-close"
              data-bs-dismiss="modal"
              aria-label="Close"
            ></button>
          </div>
          <div class="modal-body">
            <div class="mb-3">
              <label for="" class="form-label">Libelle</label>
              <input
                v-model="formProduct.libelle"
                type="text"
                class="form-control"
                name=""
                id=""
                aria-describedby="emailHelpId"
                placeholder=""
              />
              <small id="emailHelpId" class="form-text text-muted"
                >Help text</small
              >
            </div>
            <div class="mb-3">
              <label for="" class="form-label">Prix</label>
              <input
                v-model="formProduct.prix"
                type="number"
                class="form-control"
                name=""
                id=""
                aria-describedby="emailHelpId"
                placeholder=""
              />
              <small id="emailHelpId" class="form-text text-muted"
                >Help text</small
              >
            </div>
            <div class="mb-3">
              <label for="" class="form-label">Count</label>
              <input
                v-model="formProduct.count"
                type="number"
                class="form-control"
                name=""
                id=""
                aria-describedby="emailHelpId"
                placeholder=""
              />
              <small id="emailHelpId" class="form-text text-muted"
                >Help text</small
              >
            </div>

            <div class="form-check form-check-inline">
              <input
                v-model="formProduct.status"
                class="form-check-input"
                type="checkbox"
                id=""
                value="option1"
              />
              <label class="form-check-label" for="">disponible</label>
            </div>
          </div>
          <div class="modal-footer">
            <button
              @click="addProduct()"
              data-bs-dismiss="modal"
              aria-label="Close"
              type="button"
              class="btn btn-primary"
            >
              Save
            </button>
          </div>
        </div>
      </div>
    </div>

    <!-- ========== End add product ========== -->

    <div class="container">
      <div class="row">
        <div class="col-6"></div>
        <div class="col-6">
          <div class="input-group m-5">
            <span class="input-group-text" id="basic-addon1">
              <i class="bi bi-search"></i>
            </span>
            <input
              v-model="search"
              type="text"
              class="form-control"
              placeholder="product"
              aria-label="Username"
              aria-describedby="basic-addon1"
            />
          </div>
        </div>
      </div>

      <div class="row">
        <div class="col-12">
          <div class="row m-3 text-end">
            <div class="col" v-if="typeof db.account[0] == ''"></div>

            <div class="col" v-else>
              <button
                v-if="db.account[0].admin"
                class="btn btn-outline-primary"
                data-bs-toggle="modal"
                data-bs-target="#modalIdProduct"
              >
                <i class="bi bi-plus-circle"></i>
                add product
              </button>
            </div>
          </div>
          <div class="table-responsive">
            <table
              class="table table-striped table-hover table-borderless align-middle"
            >
              <thead class="table-dark">
                <tr class="bg-dark">
                  <th class="text-light">Id</th>
                  <th class="text-light">Libellé</th>
                  <th class="text-light">Prix</th>
                  <th class="text-light">Count</th>
                  <th class="text-light">Action</th>
                </tr>
              </thead>
              <tbody class="table-group-divider">
                <tr
                  v-show="
                    item.libelle
                      .toLocaleLowerCase()
                      .includes(search.toLocaleLowerCase())
                  "
                  v-for="(item, id) in products"
                  :key="id"
                >
                  <td>{{ id + 1 }}</td>
                  <td>{{ item.libelle }}</td>
                  <td>{{ item.price }}</td>
                  <td>
                    <span v-if="item.count <= 0" class="text-danger">{{
                      item.count
                    }}</span>
                    <span v-else class="text-dark">{{ item.count }}</span>
                  </td>
                  <td>
                    <button
                      @click="addToCard(item)"
                      class="btn"
                      v-if="item.status == true && item.count > 0"
                    >
                      <i class="text-success bi bi-plus-circle"></i>
                    </button>
                  </td>
                </tr>
              </tbody>
              <tfoot></tfoot>
            </table>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import db from "@/data/user.json";

export default {
  props: ["status"],
  data() {
    return {
      formProduct: {
        libelle: "",
        prix: 0,
        count: 0,
        status: false,
      },
      db: db,
      search: "",
      products: [
        { id: 1, libelle: "Iphone 6+", price: 50000, status: true, count: 5 },
        {
          id: 2,
          libelle: "Ordinateur HP",
          price: 150000,
          status: true,
          count: 10,
        },
        {
          id: 3,
          libelle: "Ecran plasma",
          price: 60000,
          status: false,
          count: 0,
        },
        {
          id: 4,
          libelle: "Groupe électrogène",
          price: 120000,
          status: true,
          count: 7,
        },
        {
          id: 5,
          libelle: "Voiture Rav 4",
          price: 5000000,
          status: true,
          count: 1,
        },
      ],
    };
  },
  methods: {
    addToCard(item) {
      item.count--;

      this.db.card.push(item);
      console.log(this.db.card);

      this.$emit("addToCard");
    },
    stateAccount() {
      setInterval(() => {
        this.db.account.at(0);
      }, 100);
    },

    addProduct() {
      const myproduct = {
        id: new Date().getTime(),
        libelle: this.formProduct.libelle,
        price: this.formProduct.prix,
        status: this.formProduct.status,
        count: this.formProduct.count,
      };

      this.products.push(myproduct);
    },
  },
  mounted() {
    this.stateAccount();
  },
};
</script>

<style></style>
