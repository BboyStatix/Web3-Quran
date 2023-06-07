# Web3 Quran
Web3 Quran dApp that pulls verses from an ethereum smart contract([0x5BfeAE4450eF5a4D86A564A606Da66dDe5D18d34](https://etherscan.io/address/0x5bfeae4450ef5a4d86a564a606da66dde5d18d34)) (created by [IslamiCity](https://www.islamicity.org/81783/islamicity-preserves-quran-as-nfts-on-the-blockchain)) instead of a centralised database (e.g. [Quran.com](https://quran.com/)).

To be clear the smart contract does not store the verses itself but rather the IPFS addresses of the verses(e.g. [](ipfs://bafybeicaqixczxfovc3weatyrakvnjwv3zsgjrblmdt4dseba2myzyioni/2.json)) so we have to fetch the verses from IPFS.

This project utilises the dweb.link public IPFS gateway to fetch the Quran verse contents (which admittedly is still quite centralised) but I plan to support fetching from self-hosted IPFS nodes in the future in shaa Allah.


## Project Setup

```sh
npm install
```

### Compile and Hot-Reload for Development

```sh
npm run dev
```

### Type-Check, Compile and Minify for Production

```sh
npm run build
```
