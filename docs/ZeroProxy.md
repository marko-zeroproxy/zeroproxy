# ZeroProxy.io Whitepaper
Born on Tue Aug  2 13:11:03 PDT 2022, created by 0x0proxy.eth  
DRAFT Version ZP-ENG-020922

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
  Framework provides a tool set especially well suited to constructing
  modular, composable, ephemeral states, such as financial
  derivatives.  By using this framework we achieve the properties of
  native collateralization, self-settlement, modularity/composability,
  and transparency.
* The ZeroProxy web3 API &mdash; a set of JavaScript tools and smart
  contract APIs that allow ZeroProxy partners and other permissioned
  actors to access ZeroProxy asset management and trading functionality.
* The ZeroProxy web2 API &mdash; The ZeroProxy web2 API provides
  ZeroProxy partners and other permissioned entities a standard web2
  RESTful interface to access ZeroProxy asset management and trading
  functionality, including support for hosted wallets.
  
## How does it work?
Before we get into the details of the architecture, let's walk through
some simple use cases.

For the sake of simplicity, we will illustrate interactions using the
web2 bridge API.

For these requests to be successful the user must first authenticate
themselves to server and unlock any relevant wallets for either a
specified number of transactions or for a defined period of time.

Server authorization by means of username and password can be
accomplished as follows:

	https://ZeroProxy.io/api/v1/auth?zeroID=...&pass=...
	
The result is a session token
(e.g. `session=deadabeefdeadbeefdeadbeef`) good for one hour (longer
periods can be requested)

To take any action other than querying the state of the ZeroChain
wallets must be unlocked for transaction signing, resulting in a
limited-use auth token, e.g.

	https://ZeroProxy.io/api/v1/unlock?chain=Solana&wallet=0xa...&sk=0x1e..&n=1&maxtime=300&session=deadbeefdeadbeefdeadbeef
	
would unlock a Solana wallet specified by `wallet` using the secret
key `sk` for one signing use `n=1` and a maximum of five minutes (300
seconds), resulting in a special-purpose auth token good only for
transactions relating to that signer,
e.g. `auth=ff031337baadcaa7031337ff`

If an `auth` token is issued with an `n` greater than one, that means
that it can be used up to `n` times. Each use must specify a `nonce=`
that increases by one each time. An invalid nonce, either a duplicate
or use out of sequence, will result in a transaction failure and an
invalidation of the `auth` token.

### Bridging Assets
One of the powerful features of ZeroProxy is its robust bridging
system, which we call BridgeMining. BridgeMining allows any supported,
standard asset class to be bridged from a supported "spoke" chain
onto the "hub" ZeroChain, and vice versa.

For example, say we wanted to bridge an NFT from Solana onto the
ZeroChain. After authenticating to the web2 bridge at
https://ZeroProxy.io/api/v1/auth and unlocking a Solana wallet, we
bridge an NFT onto the ZeroChain as so:

	https://ZeroProxy.io/api/v1/bridgeNFT?from=Solana&contract=0x0...12&tokenID=213&to=ZeroChain&wallet=0x232...a23&session=...&auth=....&nonce=1

Assuming the `session` and `auth` tokens are valid, this would
initiate the asset bridge process, temporarily locking the Solana NFT
until the asset bridge is either confirmed, in which case the asset is
locked till it comes back to the Solana chain, or is released if the
bridge is not validated, which will occasionally happen if there is a
block reorg on the Solana or ZeroChain.

If successful, the bridged NFT would be issued to the specified
wallet. A ZeroChain observer listening for events relating to the
specified wallet would receive

	EVENT:mint contract=.... tokenID=.... recipient= ...
	
### Fractionalizing NFTs
Another common operation is fractionalizing an NFT on the ZeroChain
for the purposes of writing options and then trading the options and
fractional shares. Assuming proper authentication and signer unlock,
this can be accomplished as follows:

	https://ZeroProxy.io/api/v1/fracNFT?contract=...&tokenID=...&issue=100&dragAlong=75&strike=1ETH&wallet=...&session=...&auth=...&nonce=1

Assuming success, the result would be the original NFT (as specified by
`contract` and `tokenID`) being locked in the fractionalizing escrow
contract and an ERC20 "NFT coin" being issued to the address specified
by `wallet=` with a total supply of 100, drag-along rights exercisable
by anyone owning 75% or more of the supply, and a strike price for the
drag-along call of 1 ETH (technically, 1 0x0ETH, the bridged
representation of Ethereum that is used on the ZeroChain).
  
## Architecture
![0x0proxy architecture](../assets/0x0proxyArch.svg#gh-light-mode-only)
![0x0proxy architecture](../assets/0x0proxyArchDark.svg#gh-dark-mode-only)

Break down the ZeroProxy project by architectural element

### ZeroChain
Say more about the ZeroChain here

### BridgeMining
Bridges between blockchains are essential to the operation of many
important and useful blockchain protocols. However, the problem of
securely bridging between blockchains remains an open problem, as
evidenced by the large number and high value of recent bridge attack
exploits. Since mature blockchain L1s are rarely the subject of
successful chain-level attacks, why do bridges remain vulnerable?

This is because while blockchain protocols provide relatively strong
security and consistency guarantees, connections between blockchains
necessarily exist outside such guarantees, and present low-redundancy
failure modes, in some cases requiring only the compromise of a single
signer.

We have developoed a new, highly secure approach to bridging assets
between blockchains in which the challenge of attacking the bridge
scales in difficulty with the challenge of attacking the integrity of
the underlying L1 chain.

For more information, see the [ZeroProxy Bridge Mining
Whitepaper](./BridgeMining.md).

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
