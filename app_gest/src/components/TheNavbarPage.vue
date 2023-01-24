<template>
  <main>
    <TheLoginPage></TheLoginPage>

    <nav class="nav justify-content-center shadow p-2">
      <a class="nav-link active text-dark" href="#" aria-current="page">
        <i class="bi bi-boxes"></i>
        Products
      </a>
      <a class="nav-link text-dark" href="#">
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
    return {};
  },
};
</script>
<style></style>
