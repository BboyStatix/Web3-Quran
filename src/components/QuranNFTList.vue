<script lang="ts" setup>
import { onMounted, ref } from "vue";
import nftService from "../nftService";

const NftService = new nftService();

const totalQuranVerses = ref(0);

onMounted(async () => {
  totalQuranVerses.value = await NftService.getTotalSupply();
});
</script>

<template>
  <h3>Total Qur'an NFT verses</h3>
  <div>{{ totalQuranVerses }}</div>
</template>
