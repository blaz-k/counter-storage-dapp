<template>
  <div class="text-center">
    <h1>Homepage</h1>
    <p>Counter: {{ counter }}</p>
    <p>Name: {{ someName }}</p>
    <button class="btn btn-primary" @click="contractCounter">Counter</button>

    <div class="row mt-5">
      <div class="col-md-4 offset-md-4">
        <input class="form-control" placeholder="Enter new counter value" />

        <br />

        <button class="btn btn-warning">Change Counter</button>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { ethers } from "ethers";
import { useEthers, displayEther } from "vue-dapp";
import CounterStorageAbi from "../abi/CounterStorageAbi.json";
export default {
  name: "Home",
  created() {
    this.contractGetName();
  },
  data() {
    return {
      counter: 0,
      someName: "unknown",
    };
  },
  methods: {
    async contractCounter() {
      this.counter = await this.contract.getCounter();
    },
    async contractGetName() {
      this.someName = await this.contract.getName();
    },
  },
  setup() {
    const { address, balance, chainId, isActivated, signer } = useEthers();

    const contractInterface = new ethers.utils.Interface(CounterStorageAbi);
    const contractAddress = "0x8Dec08063931947e0be134A294a0047bD9e39442";
    const contract = new ethers.Contract(
      contractAddress,
      contractInterface,
      signer.value
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
