<template>
  <HeaderComp />
  <div class="container">
    <div class="left">
      <BalanceComp :total="calculateTotal" />
      <IncomeExpenses :income="calculateIncome" :expenses="calculateExpense" />
      <AddTransaction @transactionSubmitted="handleTransactionSubmitted" />
    </div>
    <div class="right">
      <TransactionList
        :transactions="transactions"
        @transactionDeleted="handleTransactionDeleted"
      />
    </div>
  </div>
  <FooterComp />
</template>

<script>
import HeaderComp from "./components/HeaderComp.vue";
import BalanceComp from "./components/BalanceComp.vue";
import IncomeExpenses from "./components/IncomeExpenses.vue";
import TransactionList from "./components/TransactionList.vue";
import AddTransaction from "./components/AddTransaction.vue";
import FooterComp from "./components/FooterComp.vue";
import { useToast } from "vue-toastification";

const toast = useToast();

export default {
  name: "App",
  data() {
    return {
      transactions: JSON.parse(localStorage.getItem("transactions")),
      income: null,
      expense: null,
    };
  },
  components: {
    HeaderComp,
    BalanceComp,
    IncomeExpenses,
    TransactionList,
    AddTransaction,
    FooterComp,
  },
  onMounted() {
    const savedTransactions = JSON.parse(localStorage.getItem("transactions"));

    if (savedTransactions) {
      this.transactions = savedTransactions;
    }
  },
  computed: {
    calculateTotal() {
      return this.transactions.reduce((acc, transaction) => {
        return acc + transaction.amount;
      }, 0);
    },
    calculateIncome() {
      return this.transactions
        .filter((transaction) => transaction.amount > 0)
        .reduce((acc, transaction) => acc + transaction.amount, 0)
        .toFixed(2);
    },
    calculateExpense() {
      return this.transactions
        .filter((transaction) => transaction.amount < 0)
        .reduce((acc, transaction) => acc + transaction.amount, 0)
        .toFixed(2);
    },
  },
  methods: {
    handleTransactionDeleted(id) {
      this.transactions = this.transactions.filter(
        (transaction) => transaction.id !== id
      );
      this.saveTransactionsToLocalStorage();
      toast.success("Transaction deleted.");
    },
    handleTransactionSubmitted(transactionData) {
      this.transactions.push({
        id: this.generateUniqueId(),
        text: transactionData.text,
        amount: transactionData.amount,
      });

      this.saveTransactionsToLocalStorage();

      toast.success("Transaction added.");
    },
    generateUniqueId() {
      return Math.floor(Math.random() * 1000000);
    },
    saveTransactionsToLocalStorage() {
      localStorage.setItem("transactions", JSON.stringify(this.transactions));
    },
  },
};
</script>
