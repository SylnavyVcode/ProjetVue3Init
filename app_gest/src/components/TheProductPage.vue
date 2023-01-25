<template>
  <div>
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
                v-show="item.libelle.toLocaleLowerCase().includes(search.toLocaleLowerCase())" 
                v-for="(item, id) in products" :key="id">
                  
                  <td >{{ item.id }}</td>
                  <td>{{item.libelle}}</td>
                  <td>{{item.price}}</td>
                  <td>
                    <span v-if="item.count<=0" class="text-danger">{{item.count}}</span>
                    <span v-else class="text-dark">{{item.count}}</span>
                  </td>
                  <td>
                    <button 
                    @click="addToCard(item)" class="btn" 
                    v-if="(item.status == true && item.count>0)">
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
export default {
  data() {
    return {
      search:'',
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
    addToCard(item){

      item.count--

      this.$emit('addToCard')
    }
  },
};
</script>

<style></style>
