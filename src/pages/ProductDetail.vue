<script setup lang="ts">
import { useFetch } from "@vueuse/core";
import { Product } from "../models/product.model";

import { useRoute } from "vue-router";
import BaseLoading from "../components/BaseLoading.vue";
import { MDBInput, MDBBtn, MDBIcon } from "mdb-vue-ui-kit";
import {
  MDBNavbar,
  MDBNavbarItem,
  MDBNavbarBrand,
  MDBNavbarNav,
  MDBBadge,
} from "mdb-vue-ui-kit";

const {
  params: { productId },
} = useRoute();

const { isFetching, data: product } = useFetch(
  `https://fakestoreapi.com/products/${productId}`
)
  .get()
  .json<Product>();
</script>

<template>
  <MDBNavbar
    container
    expand="lg"
    bg="light"
    class="d-flex justify-content-between"
  >
    <MDBNavbarBrand class="col-md-4 col-lg-6 ml-6">
      <MDBIcon icon="mdb" iconStyle="fab" size="2x" />
    </MDBNavbarBrand>

    <MDBNavbarNav
      class="col-md-2 col-4 ml-3 mb-3 mb-lg-0 ml-4 mr-0 d-flex flex-row"
    >
      <MDBNavbarItem to="#" class="me-3 me-lg-0" linkClass="link-secondary"
        ><MDBIcon icon="shopping-cart"></MDBIcon>
      </MDBNavbarItem>
      <MDBNavbarItem to="#" class="me-3 me-lg-0" linkClass="link-secondary">
        <MDBIcon icon="bell" />
        <MDBBadge notification color="danger" pill>1</MDBBadge>
      </MDBNavbarItem>
      <MDBNavbarItem href="#" class="me-3 me-lg-0">
        <img
          src="https://mdbootstrap.com/img/Photos/Avatars/img (31).jpg"
          class="rounded-circle"
          height="22"
          alt=""
          loading="lazy"
        />
      </MDBNavbarItem>
    </MDBNavbarNav>
  </MDBNavbar>
  <v-container>
    <v-btn
      class="text-white"
      style="background: linear-gradient(-45deg, #24ff72, #9a4eff)"
      variant="text"
      @click="$router.back()"
    >
      <v-icon start icon="mdi-arrow-left"></v-icon>
      Back
    </v-btn>
    <div class="wrapper">
      <div v-if="product" class="d-flex gap-12">
        <v-img :src="product.image" width="400" class="product-img"></v-img>
        <div class="product-description">
          <span class="text-h4">{{ product.title }}</span>
          <span>{{ product.description }}</span>
          <div class="price">
            <h4><sup>$</sup>{{ product.price }}</h4>
          </div>

          <div class="buttons-group">
            <v-btn variant="text">buy now</v-btn>
            <v-btn
              class="text-white"
              style="background: linear-gradient(-45deg, #24ff72, #9a4eff)"
            >
              add to cart
            </v-btn>
          </div>
        </div>
      </div>
    </div>
  </v-container>
  <footer class="text-center text-lg-start shadow p-3 mt-3 bg-white rounded">
    <!-- Copyright -->
    <div class="text-center p-3">
      © 2023 Copyright:
      <a class="text-dark">MineShop</a>
    </div>
    <!-- Copyright -->
  </footer>
  <base-loading :loading="isFetching"></base-loading>
</template>

<style scoped>
.wrapper {
  display: flex;
  align-items: center;
  min-height: 660px;
  height: calc(100vh - 8.5em);
}
.product-img {
  border-radius: 50px !important;
  margin: 20px !important;
  padding: 50px !important;
}

.product-img {
  max-height: 37.5em;
}

.product-description {
  display: flex;
  flex-direction: column;
  gap: 3rem;
}

.gap-12 {
  gap: 3rem;
}

.buttons-group {
  margin-top: auto;
  display: flex;
  justify-content: flex-end;
  gap: 2em;
}

.price h4 {
  margin: 0;
  padding: 20px 0;
  color: #28d0b4;
  font-size: 60px;
}
</style>
