# ZeroProxy.io Whitepaper
Born on Tue Aug  2 13:11:03 PDT 2022, created by 0x0proxy.eth  
DRAFT Version ENG-020922

## Project Overview
[ZeroProxy.io](https://zeroproxy.io) is creating a better platform for
the creation, trade, and settlement of financial derivatives. 

Great progress has been made recently with bringing derivatives onto
the blockchain, but current state of the art largely replicates the
problems of the legacy financial system, resulting in centralized
exchanges with significant counterparty and settlement risk.

We are fixing these problems with a new approach that enables native
collateralization, transparent on-chain hypothecation, and the
financialization of any asset, on-chain or off, including NFTs. 

This solution is powered by the ZeroChain, an EVM-based, permissioned
blockchain designed for high-security asset bridging and the creation
and trading of financial derivatives.

## The Problem with Finance is... Derivatives

DeFi was created to democratize finance and solve the problems of the
centralized, legacy financial system.  However, no solution to the
problems of legacy finance can be meaningful if the largest underlying
problem is not addressed: financial derivatives are fundamentally
broken.

Why are financial derivatives the key to solving finance? Financial
derivatives, taken in aggregate, represent the largest financial
market on earth, and also one of the least transparent.

Approximately 2,000 Trillion USD of derivatives are traded every year,
a notional value so large as to represent a 25x multiplier on global
GDP. Most of these derivatives are centrally traded, with large
counterparty risk and little transparency. This opacity and
centralization have already led to massive market failures and crises,
the 2008 financial crisis and the 2022 crypto meltdown being only two
recent examples.

To solve the underlying problems of finance, we must do more than
bring centralized derivative exchanges on to the blockchain. We must
re-imagine what derivatives can be in a web3 world.

We believe that ideal derivatives would have the following properties:
* Universal &mdash; it should be possible to create derivatives on any
  type of asset, including tokens, NFTs, or fractionalized or
  aggregated assets.
* Multi-Chain &mdash; It should be possible to create derivatives on
  assets from any chain, and to eventually provide a mechanism to
  bring off-chain assets on to the blockchain in a robust way.
* Natively collateralized &mdash; It should be possiible to create
  derivatives that are collateralized with the native asset, as
  opposed to synthetic instruments that use a proxy asset.
* Self Settling &mdash; The settlement of natively collateralized
  derivatives should be automatic and controlled by smart contract,
  not dependent on off-chain logic or human intervention. 
* Modular and Composable &mdash; financial derivatives should be
  first-class assets, like tokens or NFTs, and should be freely
  tradable across any exchange and held in any wallet. This is in
  contrast to the largely non-composable derivatives available
  on-chain now.
* Transparent &mdash; the full chain of hypothecation of any asset
  should be visible on-chain and algorithmically enforced.
  
## The ZeroProxy Solution: Better Derivatives

We believe that there is a solution to the problem of broken financial
derivatives, and furthermore that such a solution is technically
feasible and achievable today, using well-tested underlying
technology.  This solution is built from the following elements:

* The ZeroChain &mdash; the ZeroChain is an EVM-based blockchain
  specifically designed to support the trading of financial assets and
  derivatives. Starting out as a permissioned blockchain running on
  high-performance cloud infrastructure, the ZeroChain supports
  high-throughput and low latency with a time-tested, low-power,
  proof-of-authority consensus mechanism.
* Bridge Mining &mdash; Asset bridging is central to the multi-chain,
  universal derivatives envisioned by ZeroProxy. By employing a bridge
  consensus mechanism that is similar in security and scaling
  properties to the blockchain consensus mechanism of a traditional L1,
  ZeroProxy provides strong asset security guarantees.
* The 0x0proxy Contract Framework &mdash; The 0x0proxy Contract
  Framework provides a toolset especially well suited to constructing
  modular, composable, ephemeral states, such as financial
  derivatives.  By using this framework we achive the properties of
  native collateralization, self-settlement, modularity/composability,
  and transparency.
* The ZeroProxy web3 API &mdash; a set of Javascript tools and smart
  contract APIs that allow ZeroProxy partners and other permissioned
  actors to access ZeroProxy asset management and trading functionality.
* The ZeroProxy web2 API &mdash; The ZeroProxy web2 API provides
  ZeroProxy partners and other permissioned entities a standard web2
  RESTful interface to access ZeroProxy asset management and trading
  functionality, incuding support for hosted wallets.
  
## How does it work?
Go through some examples here
  
## Architecture
![0x0proxy architecture](../assets/0x0proxyArch.svg#gh-light-mode-only)
![0x0proxy architecture](../assets/0x0proxyArchDark.svg#gh-dark-mode-only)

Break down the ZeroProxy project by architectural element

### ZeroChain
Say more about the ZeroChain here

### BridgeMining
Say more about BridgeMining here

### 0x0proxy Contract Framework

Say more about the 0x0proxy contract framework here

### ZeroProxy APIs
Say more about APIs, including:

#### ZeroProxy Web3 API
Talk about the web3 API

#### ZeroProxy Web2 API
Talk about the web2 API

![0x0proxy web2 light](../assets/0x0proxyWeb2.svg#gh-light-mode-only)
![0x0proxy web2 dark](../assets/0x0proxyWeb2Dark.svg#gh-dark-mode-only)

## Conclusions
Wrap things up
