<template>
  <h3>Add new transaction</h3>
  <form id="form" @submit.prevent="onSubmit">
    <div class="form-control">
      <label for="text">Transaction Reason</label>
      <input
        type="text"
        id="text"
        placeholder="e.g: Groceries, Income etc"
        v-model="transactionData.text"
      />
    </div>
    <div class="form-control">
      <label for="amount"
        >Amount <br />
        (negative - expense, positive - income)</label
      >
      <input
        type="number"
        id="amount"
        placeholder="Enter amount..."
        v-model="transactionData.amount"
      />
    </div>
    <button class="btn">Add transaction</button>
  </form>
</template>
<script>
import { useToast } from "vue-toastification";
const toast = useToast();

export default {
  name: "AddTransaction",
  props: {
    transactionSubmitted: Function,
  },
  data() {
    return {
      transactionData: {
        text: "",
        amaount: null,
      },
    };
  },
  methods: {
    onSubmit() {
      if (!this.transactionData.text || !this.transactionData.amount) {
        // Display a toast error message if either field is empty
        toast.error("Both fields must be filled.");
        return;
      }
      this.$emit("transactionSubmitted", this.transactionData); // Pass transactionData as a parameter
      this.transactionData.text = "";
      this.transactionData.amount = null;
    },
  },
};
</script>
