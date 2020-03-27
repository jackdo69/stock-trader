<template>
  <div class="col-sm-6 col-md-4">
    <div class="panel panel-info">
      <div class="panel-heading">
        <h3 class="panel-title">
          {{ stock.name }}
          <small
            >(Price: {{ stock.price }} | Quantity:
            {{ stock.quantiy }})</small
          >
        </h3>
      </div>
      <div class="panel-body">
        <div class="pull-left">
          <input
            type="number"
            v-model="quantity"
            class="form-control"
            placeholder="Quantity"
          />
        </div>
        <div class="pull-right">
          <button
            @click="sellStock"
            class="btn btn-success"
            :disabled="
              quantity <= 0 || !!Number.isInteger(quantity)
            "
          >
            Sell
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  import { mapActions } from "vuex";
  export default {
    props: ["stock"],
    data() {
      return {
        quantity: 0
      };
    },
    methods: {
      ...mapActions({ placeSellOrder: "sellStock" }),
      sellStock() {
        const order = {
          stockId: this.stock.id,
          stockPrice: this.stock.price,
          quantity: this.quantiy
        };
        this.placeSellOrder(order);
        this.quantity = 0;
      }
    }
  };
</script>

<style></style>
