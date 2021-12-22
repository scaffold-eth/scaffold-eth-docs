---
description: >-
  The Graph enables you to easily query data about your contract from the
  blockchain
---

# 🗄 The Graph

[The Graph](https://thegraph.com/docs) lets you process on-chain events to create a Subgraph, an easy to query graphQL endpoint!

scaffold-eth comes with a built in demo subgraph, as well as a local docker setup to run a graph-node locally.

A 15-minutes speedrun on how to integrate The Graph

{% embed url="https://youtu.be/T5ylzOTkn-Q" %}

{% hint style="warning" %}
[Requires Docker](https://www.docker.com/products/docker-desktop)&#x20;
{% endhint %}

**Step 1: Clean up previous data:**

```
yarn clean-graph-node
```

**Step 2: Spin up a local graph node by running**

```
yarn run-graph-node
```

**Step 3: Create your local subgraph by running**

```
yarn graph-create-local
```

{% hint style="info" %}
This is only required once!
{% endhint %}

**Step 4: Deploy your local subgraph by running**

```
yarn graph-ship-local
```

**Step 5: Edit your local subgraph in `packages/subgraph/src`**

Learn more about subgraph definition [here](https://thegraph.com/docs/en/developer/create-subgraph-hosted/)

**Step 6: Deploy your contracts and your subgraph in one go by running:**

```
yarn deploy-and-graph
```
