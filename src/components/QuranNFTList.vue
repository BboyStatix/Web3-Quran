<script lang="ts" setup>
import { computed, onMounted, reactive, ref } from "vue";
import nftService from "../nftService";

const VERSES_PER_PAGE = 10;

const NFTService = new nftService();

const currentPage = ref(1)

const totalQuranVerses = ref<number>(0);

const verses = reactive(new Array(VERSES_PER_PAGE));

const totalPages = computed(() => {
  return Math.ceil(totalQuranVerses.value / VERSES_PER_PAGE)
})

onMounted(async () => {
  totalQuranVerses.value = await NFTService.getTotalSupply();
  fetchVerses(currentPage.value)
});

const fetchVerses = async (currentPage: number) => {
  const startIdx = (currentPage - 1) * VERSES_PER_PAGE
  for (let i = startIdx; i < startIdx + VERSES_PER_PAGE; i++) {
    fetchVerse(i + 1).then(response => verses[i] = response);
  }
}

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
</script>

<template>
  <div>
    <div v-for="verse in verses">
      <div v-if="verse" style="margin-top: 1rem;">
        {{ verse.arabic }}
      </div>
    </div>
    <br />
    <div>Showing Verses 1-{{ VERSES_PER_PAGE }} / {{ totalQuranVerses }}</div>
    <div>Page {{ currentPage }} of {{ totalPages }}</div>
  </div>
</template>
