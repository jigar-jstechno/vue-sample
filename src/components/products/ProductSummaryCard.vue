<template>
  <div class="shop-page">
    <div class="card-item">
      <b-card
        img-alt="Image-item"
        img-top
        tag="cart"
        style="max-width: 20rem"
        class="mb-2"
      >
        <img
          class="product-image"
          :src="require('../../assets/' + product.image)"
          :data-src="require('../../assets/' + product.image1)"
          :data-hover="require('../../assets/' + product.image)"
        />
        <b-card-title>{{ product.name }}</b-card-title>

        <b-card-body>
          <b-card-text>{{ description }}</b-card-text>
        </b-card-body>

        <b-button
          v-b-modal.modal-scoped
          class="view-product-button"
          @click="$emit('view-product', product)"
          >Add to cart <span> $ {{ product.price.toFixed(2) }} </span></b-button
        >
      </b-card>
    </div>
  </div>
</template>

<script>
import jQuery from "jquery";
export default {
  // name: 'ProductSummaryCard',
  props: ["product"],

  computed: {
    description() {
      return this.product.description.substring(0, 150);
    },
  },
  mounted() {
    jQuery(document).ready(function () {
      jQuery(".product-image").hover(
        function () {
          jQuery(this).attr("src", jQuery(this).data("src"));
        },
        function () {
          jQuery(this).attr("src", jQuery(this).data("hover"));
        }
      );
    });
  },
};
</script>

<style lang="scss">
.shop-page {
  margin: 0.5rem;
}
.card-item {
  margin: 1rem;
}

.product-image {
  width: 210px;
  height: 360px;
  margin-bottom: 1rem;
}

#b-card-title {
  font-weight: bold;
}
.view-product-button {
  width: 100%;
  padding: 0.7em 0em;
  background: transparent !important;
  color: #000 !important;
  border: 1px solid rgb(217, 217, 217) !important;
  text-align: left !important;
}
.view-product-button:hover {
  // background: #e6e5e5 !important;
  color: #000;
  border: 1px solid #000 !important;
}
.view-product-button > span {
  float: right;
}
</style>


