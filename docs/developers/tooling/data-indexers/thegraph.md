---
title: TheGraph network
image: /img/socialCards/thegraph-network.jpg
---

# The Graph

Getting historical data on smart contracts can be frustrating when building a dapp. [The Graph](https://thegraph.com/) offers a powerful way to query smart contract data with open APIs known as subgraphs. Subgraphs can be created or queried by anyone, making the data available to the entire ecosystem! The Graph is powered by hundreds of independent Indexers, enabling your dapp to become truly decentralized.

Developers can use 100,000 free queries per month by using The Graph Network.

## Quick Start

Subgraphs index emitted events by default (but more functionality can be added later). A subgraph can be created in just a few minutes by following these steps:

1. Initialize your subgraph
2. Publish your subgraph to The Graph Network
3. Query from your dapp with your unique API key

Here is a step by step walk through:

## 1. Initialize You Subgraph

### Create a Subgraph on Subgraph Studio⁠

Go to the [Subgraph Studio](https://thegraph.com/studio/) and connect your wallet. Once your wallet is connected, you can begin by clicking “Create a Subgraph”. When choosing a name, it's recommended to use Title Case, including the subgraph and chain name, e.g., "MyDapp Subgraph zkSync".

You will then land on your subgraph’s page. All the CLI commands you need will be visible on the right side of the page:

### Install the Graph CLI⁠

On your local machine run the following:

```
npm install -g @graphprotocol/graph-cli
```

### Initialize your Subgraph⁠

You can copy this directly from your subgraph page to include your specific subgraph slug:

```
graph init --studio <SUBGRAPH_SLUG>
```

You’ll be prompted to provide some info on your subgraph like this:

Simply have your contract verified on the block explorer and the CLI will automatically obtain the ABI and set up your subgraph. The default settings will generate an entity for each event.

## 2. Deploy & Publish

### Deploy to Subgraph Studio⁠

First run these commands:

```bash
$ graph codegen
$ graph build
```

Then run these to authenticate and deploy your subgraph. You can copy these commands directly from your subgraph’s page in Studio to include your specific deploy key and subgraph slug:

```bash
$ graph auth --studio <DEPLOY_KEY>
$ graph deploy --studio <SUBGRAPH_SLUG>
```

You will be asked for a version label. You can enter something like v0.0.1, but you’re free to choose the format.

### Test your subgraph⁠

You can test your subgraph by making a sample query in the playground section. The Details tab will show you an API endpoint. You can use that endpoint to test from your dapp.

### Publish Your Subgraph to The Graph’s Decentralized Network

Once your subgraph is ready to be put into production, you can publish it to the decentralized network. On your subgraph’s page in Subgraph Studio, click on the Publish button:

Before you can query your subgraph, Indexers need to begin serving queries on it. In order to streamline this process, you can curate your own subgraph using GRT.

When publishing, you’ll see the option to curate your subgraph. As of May 2024, it is recommended that you curate your own subgraph with at least 3,000 GRT to ensure that it is indexed and available for querying as soon as possible.

> **Note:** The Graph's smart contracts are all on Arbitrum One, even though your subgraph is indexing data from Ethereum, BSC or any other [supported chain](https://thegraph.com/docs/en/developing/supported-networks/).

## 3. Query your Subgraph

Congratulations! You can now query your subgraph on the decentralized network!

For any subgraph on the decentralized network, you can start querying it by passing a GraphQL query into the subgraph’s query URL which can be found at the top of its Explorer page.

Here’s an example from the [CryptoPunks Ethereum subgraph](https://thegraph.com/explorer/subgraphs/HdVdERFUe8h61vm2fDyycHgxjsde5PbB832NHgJfZNqK) by Messari:

The query URL for this subgraph is:

`https://gateway-arbitrum.network.thegraph.com/api/`**[api-key]**`/subgraphs/id/HdVdERFUe8h61vm2fDyycgxjsde5PbB832NHgJfZNqK`

Now, you simply need to  fill in your own API Key to start sending GraphQL queries to this endpoint.

### Getting your own API Key

In Subgraph Studio, you’ll see the “API Keys” menu at the top of the page. Here you can create API Keys.

## Appendix

### Sample Query

This query shows the most expensive CryptoPunks sold.

```graphql
{
  trades(orderBy: priceETH, orderDirection: desc) {
    priceETH
    tokenId
  }
}
```

Passing this into the query URL returns this result:

```
{
  "data": {
    "trades": [
      {
        "priceETH": "124457.067524886018255505",
        "tokenId": "9998"
      },
      {
        "priceETH": "8000",
        "tokenId": "5822"
      },
//      ...
```

### Sample code

```jsx
const axios = require("axios");

const graphqlQuery = `{
  trades(orderBy: priceETH, orderDirection: desc) {
    priceETH
    tokenId
  }
}`;
const queryUrl =
  "https://gateway-arbitrum.network.thegraph.com/api/[api-key]/subgraphs/id/HdVdERFUe8h61vm2fDyycHgxjsde5PbB832NHgJfZNqK";

const graphQLRequest = {
  method: "post",
  url: queryUrl,
  data: {
    query: graphqlQuery,
  },
};

// Send the GraphQL query
axios(graphQLRequest)
  .then((response) => {
    // Handle the response here
    const data = response.data.data;
    console.log(data);
  })
  .catch((error) => {
    // Handle any errors
    console.error(error);
  });
```

### Additional resources:

- To explore all the ways you can optimize & customize your subgraph for better performance, read more about [creating a subgraph here](https://thegraph.com/docs/en/developing/creating-a-subgraph/).
- For more information about querying data from your subgraph, read more [here](https://thegraph.com/docs/en/querying/querying-the-graph/).

As a dapp developer, retrieving on-chain data for your dapp can be challenging because you will most likely:

1. Consume your RPC provider quota with calls.
2. Need to implement error handling on multiple levels.
3. Define creative strategies to avoid UX impacts when managing a high volume of data.

The Graph is a decentralized data indexer provider that indexes the Linea blockchain for you and exposes on-chain data through an HTTPS API.

We run The Graph indexers on Linea to allow you to leverage the power of this technology. :::info[update]

TheGraph is now live with Linea Mainnet! For more information, take a look at their official [documentation](https://thegraph.com/docs/en/)

:::
