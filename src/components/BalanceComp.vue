<template>
  <h4>Your Balance</h4>
  <h1 id="balance">Rs {{ total }}</h1>
</template>
<script>
export default {
  name: "BalanceComp",
  props: {
    total: Number,
  },
};
</script>
