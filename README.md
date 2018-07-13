Personal Notes to build a mini BTC for my team

## What is this

This project is an experiment of creating a 'mini bitcoin' on my own, essentially forking btc to a alt-coin. I cloned from the official bitcoin code, adjusted a few parameters, added a few print commands to make the output more verbose.

Bitcoin node can be started in three different modes, mainnet, testnet and regtest. In this codebase, I only touched the testnet portion. Thus the code is only meant to be started in 'testnet' mode. Moreover the bitcoin node will not connect to any existing public nodes. They live in their little world, and keep in sync with each other.

Diffculty level has been set to a very low level. If there are many nodes are consistently mining (in our case using the generate cli command), the difficulty will still be adjusted upwards.

## How to start testing

To start the first bitcoin node
* in one terminal, navigate to src folder, run ./bitcoind -port=19000 -rpcport=19001 -datadir=1/

To start the second bitcoin node and ask it to connect to the first node
* in 2nd terminal, navigate to src folder, run ./bitcoind -port=19010 -rpcport=19011 -connect=127.0.0.1:19000 -datadir=2/

To use bitcoin-cli, in 3rd terminal, navigate to src folder, 
* to view current block chain info, `./bitcoin-cli -rpcport=19001 -datadir=1/ getblockchaininfo`
* to ask the first node to mine a block `./bitcoin-cli -rpcport=19001 -datadir=1/ generate 1`
* to ask the second node to mine 3 blocks `./bitcoin-cli -rpcport=19011 -datadir=2/ generate 3`
* try to see how new blocks' info are propagated between nodes

The current blockchain may already contain some blocks that I 'mined' in the past. The difficulty is adjusted slightly to fit to my MacBook Pro. 

To start from an clean empty blockchain
* in src folder, run `rm -rf 1/testnet3/ 1/blocks/ 2/testnet3/ 2/blocks/`
* bitcoin-cli's getblockchaininfo will return blocks=0, i.e. no block on the chain

### How to build these from scratch on Mac

I followed this document https://github.com/bitcoin/bitcoin/blob/master/doc/build-osx.md

First, prepare the environment on Mac
* xcode-select --install
* install homebrew (follow my other guide on installation)
* brew install automake berkeley-db4 libtool boost miniupnpc openssl pkg-config protobuf python qt libevent qrencode
  * if python is installed seperatly before hand, remove it if you like
* brew install librsvg

Clone and Preconfigure the bitcoin code
* git clone https://github.com/bitcoin.bitcoin
* ./autogen.sh
* ./configure --without-gui

Build the code (for every changes we make)
* on top level (bitcoin directory), run `make`


## References

to be added later
