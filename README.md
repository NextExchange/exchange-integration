##
# NEXT INTEGRATION GUIDE

NEXT developed the NEXT.chain and combined the best blockchain technologies with a focus on speed, scalability and security. We took take the Bitcoin Core code as a basis, placed Masternodes on it like Dash and implemented assets and smart contracts like Ethereum their ERC20.

The NEXT coin is the native coin, like BTC or ETH. NEXT is highly decentralized and currently has a circulation supply of ~16M. Since the blockchain is a combination of Proof of Work and Proof of Stake consensus algorithms, anyone can mine or host a node and receive NEXT as network contribution reward. A node requires 25.000 NEXT coins. Merge mining NEXT with BTC is possible, since we&#39;re based on the SHA-256 algorithm. 45% of our network rewards go to miners, 45% to Masternodes and 10% is reserved.

# Technical specifications

| Ticker | NEXT |
| --- | --- |
| Algorithm | SHA256 (X11) |
| Consensus | Proof-of-Work / Proof-of-Stake combined |
| Maximum Supply | 30,000,000 |
| Block Time | ~30 seconds |
| Transactions Per Second | over 10K+ |
| Lightning Network | Yes |
| Instant Transactions | Yes |
| Private Transactions | Yes |
| Atomic Swap | Yes |
| Blockchain bridge | Yes |


### What are the standard ports for integrating NEXT?

NEXT uses the following ports:

| --- | --- |
| RPC Port:    |         7077 |
| P2P Port:    |         7078 |
| Testnet RPC: |        17077 |
| Testnet P2P: |        17078 |

Both are TCP. While you do not need to have them publicly exposed / forwarded, doing-so does not create any security risk and allows your node to further contribute to the security of the network by being discoverable by other nodes.

### Do you have any recommendations for integrating your wallet?

We recommend a minimum of 6 confirmations for deposits / withdrawals (_which takes_ approx. 90 seconds). Notifications usually occur almost real-time for transactions, with blocks being _verified_ every 30 seconds.

If possible, use either Bech32 or SegWit addresses, and batch-process transactions.

### Is there a max capacity?

It genuinely depends on the capacity of the server, and the optimization of the software integrating with it. Look at your Bitcoin server utilization for a good indication.


### What parameters are recommended when /_or_ running a wallet?

The NEXT node directly connects to the NEXT.chain and will download every block straight away, addthe following to ~/.next/nextcoin.conf:

# ~/.next/nextcoin.conf
`
server=1
listen=1
daemon=1
txindex=1
rpcallowip=127.0.0.1
maxconnections=300
addnode=seed.next.2srv.io
`

### What are the hardware requirements to run a single node?

A single node can happily seed _on a server with_ hardware as low as an Intel Atom with 4GB RAM and 40GB HDD. The wallet _itself_ runs on any Windows, Linux or Mac computer.

The most important element to think about when setting up a server is storage space. Right now the NEXT chain is only 1Gb big, but this can grow towards 100Gb or more. Monitor the size of the chain, and adjust your server space accordingly._

Once your server is up and running, please regularly clear the_ debug.log _file located in_ ~/.next. This file can grow big over time and will become too heavy. Nextd can and should always be running as a &#39;non-privileged user&#39; from within the home directory, and sudo access is not required at any time.

### How to back-up or restore the wallet?

As per Bitcoin, backing up the private keys or wallet.dat is sufficient. We recommend where possible you use a multi signature wallet.

### Are there any known restrictions or issues we should know _of_?

As of 3.4.x, NEXT has implemented upstream **Bitcoin Core 0.17 RPC** formats. Common calls that exchanges / pools need to know about is that getinfo has been replaced by:

- getblockchaininfo
- getnetworkinfo
- getwalletinfo
- getmininginfo

In addition, signrawtransaction has been split in to two calls:

- signrawtransactionwithkey
- signrawtransactionwithwallet

signrawtransactionwithkey requires private keys to be passed in and does not use the wallet for any signing. signrawtransactionwithwallet uses the wallet to sign a raw transaction and does not have any parameters to take private keys.

We strongly advise also being aware of this when where integrators are using the RPC calls directly, this call will no doubt be deprecated across other wallets going forward, as they bring themselves up to speed with the Bitcoin Core codebase.

Where existing products and services are using signrawtransaction, you should simply use signrawtransactionwithwallet instead.

In addition, if you&#39;ve been making use of the ismine value in validateaddress, you&#39;ll want to call getaddressinfo instead, as the result is being returned there.

To get the full API call list, please visit:
[https://en.bitcoin.it/wiki/Original\_Bitcoin\_client/API\_calls\_list](https://en.bitcoin.it/wiki/Original_Bitcoin_client/API_calls_list)

### What is the NEXT explorer?

Please visit [https://explore.next.exchange](https://explore.next.exchange) or [http://www.nextplorer.xyz](http://www.nextplorer.xyz) or [https://nextexplorer.io](https://nextexplorer.io).

### What are the advantages of running a full node?

We recommend all exchanges _or_ products _to_ run their own node they can use for API calls, especially if they are expecting decent volume. This can be run inside a virtualized environment without any additional configuration requirements.

Running your own node will allow the best possible performance for your product. Although there are NEXT nodes, very few run the Insight API on top of it for Blockchain integration.

The latest wallet binaries can be found at: [https://github.com/NextExchange/next-wallet-desktop-app](https://github.com/NextExchange/next-wallet-desktop-app)

### Who should we contact for additional technical support?

All of our developers and most of our community operate out of Telegram. [https://t.me/next_exchange](https://t.me/next_exchange). For additional assistance, please contact [dev@next.exchange](mailto:dev@next.exchange).

### Where can I find the original logo files?

You can download the NEXT logo in a variety of formats from:

[https://github.com/NextExchange/media](https://github.com/NextExchange/media)
