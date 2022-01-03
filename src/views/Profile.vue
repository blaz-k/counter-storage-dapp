<template>
  <div class="container text-center">
    <h2>Profile</h2>

    <p>Address: {{ address }}</p>
    <p>Balance: {{ displayEther(balance) }} MATIC</p>
    <p>chain Id : {{ chainId }}</p>
    <p>chain Id : {{ showChainName }}</p>

    <p v-if="chainId != 80001">You are on the wrong network</p>
  </div>
</template>

<script lang="ts">
import { useEthers, displayEther } from "vue-dapp";

export default {
  name: "Profile",
  computed: {
    showChainName() {
      if (this.chainId === 1) {
        return "Ethereum";
      } else if (this.chainId === 80001) {
        return "Mumbai";
      }
    },
  },

  setup() {
    const { address, balance, chainId, isActivated } = useEthers();

    return {
      address,
      balance,
      chainId,
      isActivated,

      displayEther,
    };
  },
};
</script>
