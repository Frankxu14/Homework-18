# Homework 18
## Proof of Authority Development Chain
## Frank Xu


## Background and Brief Description of Project
In this assignment, I as the new IT developer of ZBank, set up a private, custom testnet blockchain named foxxnet, and to explore the potentials of Clique Proof of Authority algorithm.

To start, we install the dependencies and environment configuration including Geth and Puppeth command-line tools.

Download and install Geth & Tools 1.9.7 from the Go Ethereum Tools page at https://geth.ethereum.org/downloads/
(Go Ethereum is one of the three original implementations of the Ethereum protocol. It is written in Go, fully open-source and licensed under the GNU LGPL v3.)

For this Homework, we create a project repository folder named "Foxxnet", as we name our private, custom testnet blockchain "foxxnet."

## Create New Account Addresses for Node 1 and Node 2
First, in your local terminal (or gitbash under Windows environment) create accounts for two nodes for the network, by the following commands:
./geth account new --datadir node1
./geth account new --datadir node2

The new accounts are locked with a password. please enter a password, please keep the password seperate and secured.

Geth will generate new keys, public addresses of the new keys, and store the secret keys under the node1/keystore and node2/keystore subfolders, respectively.
See Screen Shot-Geth new nodes.

## Configure New Genesis Block
Second, run ./puppeth command, name the new, private blockchain network as "foxxnet", and choose the option to "Configure new genesis" block.

As we choose to test the proof-of-authority consensus engine, choose 2. "Clique -Proof-of-Authority" consensus algorithm.

On the follow-up prompts of which accounts should be allowed to seal and be prefunded, paste both account public addresses (without "Ox") from the stop above once a time.
(As there is no  block rewards in PoA, we'll need to pre-fund.)

Choose "no" for pre-funding the pre-compiled accounts (0x1 .. 0xff) with wei, and specify the chain/network ID. Here we enter: 123.


## Export Genesis Configurations
Next, we export the genesis configurations. As we choose Proof-of-Authority consensus algorithm, Puppeth would fail to create "Aleth chain spec" and "Parity chain spec." It will create two files, including "foxxnet.json" having saved native genesis chain spec. See Foxxnet/foxxnet.json; Screen Shot-Puppeth.

Next, with Geth command, we initialize each node with the new foxxnet.json configuration and consensus algorithm information. See Screen Shot-Initialize foxxnet nodes.

## Unlock and Enable Mining
To run the first node, unlock the account, enable mining, by the following command:
./geth --datadir node1 --unlock "3bAbE50720334f00753872a1c5daACf2Bce4204f" --mine --rpc --allow-insecure-unlock
(Note, the first node RPC enabled (with command line --prc)
See, Screen Shot-Unlock and commit mining.

In a seperate terminal, we set a peer, remote port for node 2, using first node's enode address as the bootnode.

We unlock the account and enable mining on the second node by the following command:
./geth --datadir node2 --unlock "759c1313AFc11AfD917FD6030EB423CE414C9D26" --mine --port 30304 --bootnodes "enode://94741bfcbbf3929343e42a5485373d759a3dac837f9f936042143e7cfa4542ce7bcdb264c9c90c9d83ebe8eecf945bd36478775566b7cc0fcc18e066dc21b28f@127.0.0.1:30303" --allow-insecure-unlock --nodiscover 


## MyCrpto Wallet Test Transaction

To use the MyCrypto GUI wallet to connect to the node with the exposed RPC port, we change network, and enter Custom Network naming it "foxnnet" with pre-set blockchain ID. See Screen Shot-foxxnet.

By importing the keystore file from node1/keystore directory into MyCrypto, entering password for node1 we initially set in steps above, we import the private key and are able to update Account Address and Account Balance. See, Screen Shot-MyCrypto Wallet.

In Mycrypto Wallet send a transaction from the node1 account to the node2 account public address. Copying the transaction hash and paste it into the "TX Status" section. For the transaction metadata (status, TX hash, block number, etc), see Screen Shot-TX Hash.




