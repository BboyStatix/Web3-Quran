# Web3 Quran
Quran dApp that pulls verses from an ethereum [smart contract](https://etherscan.io/address/0x5bfeae4450ef5a4d86a564a606da66dde5d18d34) created by [IslamiCity](https://www.islamicity.org/81783/islamicity-preserves-quran-as-nfts-on-the-blockchain).

To be clear the smart contract does not store the verses itself but rather the IPFS addresses of the verses(e.g. ipfs://bafybeicaqixczxfovc3weatyrakvnjwv3zsgjrblmdt4dseba2myzyioni/2.json) so we have to fetch the verses from IPFS.

This project utilises the `dweb.link` public IPFS gateway to fetch the Quran verse contents. For example the above IPFS URI can be accessed via the gateway at https://dweb.link/ipfs/bafybeicaqixczxfovc3weatyrakvnjwv3zsgjrblmdt4dseba2myzyioni/2.json.

Admittedly using an IPFS gateway is still quite centralised but I plan to support fetching from self-hosted IPFS nodes in the future in shaa Allah.

Technically the Quran is already preserved in a decentralised manner in the hearts of the people. So even if all the Web2 Quran websites were taken down and access to physical mushafs were restricted, you'd still have to take out all the human full nodes(the huffaz) that have it memorised from cover to cover.


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
