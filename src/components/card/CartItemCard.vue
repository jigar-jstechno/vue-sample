<template>
  <div class="shopping-card">
    <b-card>
      <b-table-simple hover small caption-top responsive>
        <b-tbody>
          <b-tr class="mobile-tr">
            <b-th>{{ product.name }}</b-th>
            <b-th>{{ description }}</b-th>
            <b-th class="button-container-cart">
              <b-button variant="" class="remove" @click="removeFromCart()">
                -
              </b-button>
              {{ product_total }}

              <b-button variant="" class="add" @click="addToCart()">
                +
              </b-button>
            </b-th>
            <b-th>$ {{ item_cost.toFixed(2) }}</b-th>
            <b-td>
              <b-button
                variant="danger"
                class="delete-product-one"
                @click="deleteFromCart(product)"
                >Delete</b-button
              >
            </b-td>
          </b-tr>
        </b-tbody>
        <b-tfoot>
          <b-tr>
            <b-td colspan="7" variant="secondary" class="mobile-tc text-right">
              <b>Total cost: {{ item_cost.toFixed(2) }}</b>
            </b-td>
          </b-tr>
        </b-tfoot>
      </b-table-simple>
    </b-card>
  </div>
</template>

<script>
export default {
  props: ["product"],

  methods: {
    addToCart() {
      this.$store.commit("addToCart", this.product);
    },
    removeFromCart() {
      this.$store.commit("removeFromCart", this.product);
    },

    deleteFromCart(product) {
      this.$store.commit("deleteFromCart", product);
    },
  },
  computed: {
    description() {
      return this.product.description.substring(0, 120);
    },
    item_cost() {
      return this.product.price * this.product.quantity;
    },
    product_total() {
      return this.$store.getters.productQuantity(this.product);
    },
  },
};
</script>

<style lang="scss">
.shopping-card {
  margin: 1rem;
  margin: 15px;
}
.mobile-tr > th,
.mobile-tr > td {
  border-top: none;
}
.delete-product-one {
  vertical-align: middle !important;
  margin-top: 1rem;
  float: right;
}
.button-container-cart {
  float: right !important;
}
.table-responsive {
  margin-bottom: 0px;
}

@media only screen and (max-width: 600px) {
  .mobile-tr {
    display: grid !important;
    border: none;
  }

  .mobile-tr > th,
  .mobile-tr > td {
    border-top: none;
  }
  .button-container-cart {
    float: unset !important;
  }
  .delete-product-one {
    vertical-align: middle !important;
    margin-top: 0rem;
    margin-bottom: 1rem;
    float: unset;
  }
  // .shopping-card {
  //   margin: 15px;
  // }
  .table-responsive {
    margin-bottom: 0px;
  }
  .mobile-tc {
    padding-right: 15px !important;
  }
}
</style>



