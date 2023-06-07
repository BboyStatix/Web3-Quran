<script lang="ts" setup>
import { onMounted, reactive, ref } from "vue";
import nftService from "../nftService";

const VERSES_PER_PAGE = 7;

const NFTService = new nftService();

const totalQuranVerses = ref(0);

const verses = reactive(new Array(VERSES_PER_PAGE));

const fetchVerse = async (verseNo: number) => {
  let tokenIPFSURI: string;
  try {
    tokenIPFSURI = await NFTService.getTokenURI(verseNo);
  } catch (e) {
    console.error("Failed to fetch token URI from smart contract");
    throw e;
  }

  try {
    const response = await fetch(
      `${import.meta.env.VITE_IPFS_GATEWAY_ENDPOINT}/${tokenIPFSURI.replace(
        "ipfs://",
        ""
      )}`
    );
    if (!response.ok) throw new Error("Failed to fetch verse contents");
    const data = await response.json();
    return data;
  } catch (e) {
    console.error("Failed to fetch verse from IPFS");
    throw e;
  }
};

onMounted(async () => {
  totalQuranVerses.value = await NFTService.getTotalSupply();

  for (let i = 1; i <= VERSES_PER_PAGE; i++) {
    const verse = await fetchVerse(i);
    verses[i] = verse;
  }
});
</script>

<template>
  <div v-for="verse in verses">
    <div v-if="verse">
      {{ verse.arabic }}
    </div>
  </div>
  <br />
  <div>Showing Verses 1-{{ VERSES_PER_PAGE }} / {{ totalQuranVerses }}</div>
</template>
