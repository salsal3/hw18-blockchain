# Homework 18: Blockchain
---

## The Gluten Matrix

Welcome to Zenith, the ZBank blockchain test network built with the Clique proof-of-authority concensus protocol. Before running the nodes, be sure to follow the [blockchain installation guide](https://github.com/RutgersCodingBootcamp/RUT-VIRT-FIN-PT-05-2021-U-LOL/blob/master/Supplemental_Material/18-Blockchain/blockchain-install-guide.md). There you'll find instructions on how to install, Go Ethereum, which we'll use to run the blockchain nodes, and MyCrypto, where we'll access our digital wallets and make transactions.

## Account Setup
To create accounts for our test nodes, we use the `./geth` command from Go Ethereum. In the  terminal, `cd` into the `blockchain-tools` folder and enter the following:
`./geth account new --datadir "node_name"`

For the purposes of our testing, there are only two nodes, znode1 and znode2, and a password is created for each one (`zebra` and `zero` respectively). It's important to save the "Public address of the key" and keep them handy for easy access.
![Account Setup](../hw18-blockchain/Screenshots/ss1-znode1-setup.png)
![Account Setup](../hw18-blockchain/Screenshots/ss1-znode2-setup.png)

## Network Setup
Next is setting up the network. For that, we use the command `./puppeth` - also from Go Ethereum. A series of prompts guide the setup process, and we use the following configurations:
1. Network name: *zenith*
2. *Configure new genesis*
3. *Create new genesis from scratch*
4. Consensus engine: *2* (for *Clique - proof-of-authority*)
5. Seconds per block (blocktime): *15* (default)
6. *Enter the public addresses of both nodes. Puppeth automatically populates "0x" to the beginning, so copy and paste the portion of the public addresses that follow those characters.*
7. *Enter both addresses again*
8. Precompile addresses: *no*
9. Chain/network ID: *26*
![Puppeth Config](../hw18-blockchain/Screenshots/ss2a-puppeth-config.png)

### Export Configurations
After creating the network, follow the prompts to "Manage existing genesis" and "Export genesis configurations", then hit Enter to save the genesis specs to the current "blockchain-tools" folder. Two files titled "zenith.json" and "zenith-harmony.json" will be created. We won't be using the "harmony" file, so that can be safely deleted.
![Export Config](../hw18-blockchain/Screenshots/ss2b-export-config.png)

### Initalize the Nodes
Last part of the network setup is to initialize the nodes, using the following commands:
`./geth init zenith.json --datadir znode1`
`./geth init zenith.json --datadir znode2`
![Account Setup](../hw18-blockchain/Screenshots/ss3-znode1-init.png)
![Account Setup](../hw18-blockchain/Screenshots/ss3-znode2-init.png)

## Running the Blockchain
Now on to the fun stuff! In order to run our nodes, the following commands are used to run both of the nodes:
- `./geth --datadir znode1 --unlock "6788eA7bf01E7C34F25A68F2a9e7fA75EbAb6574" --mine --miner.threads 1`
    - The password again is "zebra".
- `./geth --datadir znode2 --unlock "6d6D07547E3b6F3ba7f54aE910daf2dC106125cd" --port 30301 --rpc --bootnodes "enode://22c4c09a07e4f60506279f64a84961ad10db276ffa4443bd4378b810bdc8303201511e568fa86f5ce145456a3e754b90fe31a38321867ba1e72939276ae7926e@127.0.0.1:30303" --ipcdisable --allow-insecure-unlock`
    - The password again is "zero".
![Running znode1](../hw18-blockchain/Screenshots/ss4-running-znode1.png)
![Running znode2](../hw18-blockchain/Screenshots/ss4-running-znode2.png)

### Geth Command-line Options
The following command-line options are used in the `./geth` commands when running the nodes. Definitions are taken from the [Go Ethereum Documentation](https://geth.ethereum.org/docs/interface/command-line-options), where you can read about all of the options available.
- `--unlock`: comma separated list of accounts to unlock.
- `--mine`: enables mining for the first node.
- `--miner.threads`: sets the number of CPU threads to use for mining.
    - Since we're only communicating between two nodes, this is set to `1`.
- `--port`: network listening port (default: 30303). Each node is set on a different port (for our network, 30303 for znode1 and 30304 znode2).
- `--rpc`: enables the http-rpc server, allowing `znode2` to connect to the blockchain.
- `--bootnodes`: enode URL of the first node is set, allowing peer-to-peer discovery bootstrap.
    - The enode:// address of the first node should be in quotes, and should include `enode://` and `@127.0.0.1:30303`.
- `--ipcdisable`: disables the IPC-RPC server.
    - This is necessary for Microsoft Windows.
- `--allow-insecure-unlock`: allow insecure account unlocking when account-related RPCs are exposed by http.

## MyCrypto
With both nodes up and running, we're ready to make a transaction. In the MyCrypto program, at the bottom of the sidebar, click on "Change Network". Scroll to the bottom again and click on "Add Custom Node". In the resulting screen, under "Network", select "Custom" and enter the information for znode1.
![MyCrypto Setup](../hw18-blockchain/Screenshots/ss5-mycrypto-setup.png)

Save the settings, then select "Change Network" once more, this time selecting the newly created zenith network. It may take a few tries, or you may need to restart the MyCrypto program entirely.

---
### Create a repository, and instructions for launching the chain

* Create a `README.md` in your project directory and create documentation that explains how to start the network.

* ~~Remember to include any environment setup instructions and dependencies.~~

* ~~Be sure to include all of the `geth` flags required to get both nodes to mine and explain what they mean.~~

* ~~Explain the configuration of the network, such as it's blocktime, chain ID, account passwords, ports, etc.~~

* Explain how to connect MyCrypto to your network and demonstrate (via screenshots and steps) and send a transaction.

* Upload the code, including the `networkname.json` and node folders.

~~puppeth confirmation, network name~~
~~mycrypto with custom node settings~~
~~prefunded wallet~~
~~transaction = pending~~
transaction = successful