<template>
  <div class="text-center">
    <h1>Homepage</h1>
    <p>Counter: {{ counter }}</p>
    <p>Name: {{ someName }}</p>
    <button class="btn btn-primary" @click="add">Count</button>
  </div>
</template>

<script lang="ts">
import { ethers } from "ethers";
import { useEthers, displayEther } from "vue-dapp";
import CounterStorageAbi from "../abi/CounterStorageAbi.json";
export default {
  name: "Home",
  data() {
    return {
      counter: 0,
      someName: "unknown",
    };
  },
  setup() {
    const { address, balance, chainId, isActivated, provider } = useEthers();

    const contractInterface = new ethers.utils.Interface(CounterStorageAbi);
    const contractAddress = "0x8Dec08063931947e0be134A294a0047bD9e39442";
    const contract = new ethers.Contract(
      contractAddress,
      contractInterface,
      provider.value
    );

    return {
      address,
      balance,
      chainId,
      isActivated,
      displayEther,
      contract,
    };
  },
};
</script>
