
Run a Stacks and a Bitcoin node, together, on Docker.

Stacks needs to use the Bitcoin node, and by default when you run a Stacks node you will be using a public Bitcoin node. Here you can run both nodes together and configured so your Stacks node uses your own bitcoin node.

## Why run Stacks node with your own Bitcoin node?

Because running your own Bitcoin node will give you higher security and improved perfomance.

* **Improved perfomance**: The Bitcoin node will serve you blocks faster, as well as UTXOs for your miner (if you run one).
* **Higher security**: The Bitcoin node will also have validated all bitcoin transactions the Stacks node consumes. If you don't run your own Bitcoin node, you're relying on the SPV headers to vouch for the validity of Bitcoin blocks.


## Requirements
You will need docker installed. If you don't have it, you can easily get it [here](https://docs.docker.com/get-docker/).

Bitcoin's blockchain keeps growing but currently takes up about 500GB of space. You can choose to store this in this same drive you are running docker or store these files in another drive or NAS by simply removing the comment on [line 12 of the docker-compose.yml](docker-compose.yml#L12) file

## Instructions

1. Download this repository

    `git clone https://github.com/ungtb10d/stacks-bitcoin-doublenode.git && cd stacks-bitcoin-doublenode`

2. Run
    `docker-compose up -d`

To shut it down type `docker-compose down`.

## Monitor

You can view what the nodes are doing with:

```
docker logs -f stacks-node
docker logs -f bitcoin-core
```

## Security note

Stacks and Bitcoin RPC credentials should match. They do by default in this repository.
It's safe to use this default password as long you don't make the bitcoin node publicly available to the Internet, which by default it is not.

If you do however manually edit this docker-compose file to open the Bitcoin ports 8333 and 8334 to the Internet, you should change the default password to something of your choosing. The password needs to be changed in two files:

[/bitcoin.conf (line 2)](https://github.com/ungtb10d/stacks-bitcoin-doublenode/blob/main/bitcoin.conf#L2)  
[/stacks-node/config/mainnet/Config.toml (line 13)](https://github.com/ungtb10d/stacks-bitcoin-doublenode/blob/main/stacks-node/config/mainnet/Config.toml#L13)  
# Stacks-Bitcoin Double Node on Docker
