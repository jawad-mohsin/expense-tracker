<template>
  <h3>Transaction History</h3>
  <ul id="list" class="list">
    <li
      v-for="transaction in transactions"
      :key="transaction.id"
      :class="transaction.amount < 0 ? 'minus' : 'plus'"
    >
      {{ transaction.text }} <span>Rs {{ transaction.amount }}</span
      ><button class="delete-btn" @click="deleteTransaction(transaction.id)">
        <lord-icon
          src="https://cdn.lordicon.com/skkahier.json"
          trigger="in"
          delay="1500"
          state="in-trash-empty"
          style="width: 25px; height: 25px"
        ></lord-icon>
      </button>
    </li>
  </ul>
</template>
<script>
export default {
  name: "TransactionList",
  props: {
    transactions: Array,
    transactionDeleted: Function,
  },
  methods: {
    deleteTransaction(id) {
      this.$emit("transactionDeleted", id); // Pass transactionData as a parameter
    },
  },
};
</script>
