Whenever you see `gaia` or `gaiad` used make sure to replace with whatever node you are installing. Both `app.toml` and `config.toml` have been heavily commented with useful information. Please read through both of these files carefully.


## app.toml

Direct yourself to your node's configuation folder.  
  
`cd ~/.gaiad/config/`  
  
Set your preferred pruning settings. Here is an example set of commands to run while located inside your `config` directory. Update values to your preference and space needs (the numbers below are for tight pruning). If you ever find your chain data is taking up too much space, consider using tools such as [cosmprund](https://github.com/binaryholdings/cosmprund).  If you are running an archive node then you can ignore this:  
  
`pruning="custom" && \`  
`pruning_keep_recent=107 && \`  
`pruning_keep_every=0 && \`  
`pruning_interval=73 && \`  
`sed -i -e "s/^pruning *=.*/pruning = \"$pruning\"/" app.toml && \`  
`sed -i -e "s/^pruning-keep-recent *=.*/pruning-keep-recent = \"$pruning_keep_recent\"/" app.toml && \`  
`sed -i -e "s/^pruning-keep-every *=.*/pruning-keep-every = \"$pruning_keep_every\"/" app.toml && \`  
`sed -i -e "s/^pruning-interval *=.*/pruning-interval = \"$pruning_interval\"/" app.toml`  
  
It's time to edit `app.toml` if you need to enable, disable, or edit ports for API and gRPC. Also be mindful of minimum gas fees, especially if you are a valiadtor. Refer to [official docs](https://github.com/cosmos/gaia/blob/main/docs/hub-tutorials/join-mainnet.md) for more information. To get started open the `app.toml` file.   
  
`nano ~/.gaia/config/app.toml`  
  
CTRL+X and save any changes you made.  
  
  
## config.toml  

Direct yourself to your node's configuation folder.  
  
`cd ~/.gaiad/config/`  
`nano config.toml`  

This is the main configuration file for your node. If you are using default ports there is not much that needs changed here. If you are using custom ports, be sure to edit them here and verify UFW settings before launching your node.

If you wish to access your node remotely from a local machine, you'll also need to expose the node's RPC by changing the IP address to `0.0.0.0` in the RPC section  
  
`# TCP or UNIX socket address for the RPC server to listen on`  
`laddr = "tcp://0.0.0.0:26657"`  
  
You'll also need to add peers before you start syncing. Most blockchains will have a network repository featuring peer lists, genesis files, etc., Another great option is to use [Polkachu](https://polkachu.com/networks/cosmos) if they have the chain resources available on their website. You can find resources for state sync, snapshot sync, peers, etc.,
  
When adding peers, make they are placed inbetween quotes, divided by commas with no spaces. For example: 
  
`persistent_peers = "cf10a45ead9e76d45b06dee97ef779e65103c78e@3.128.185.235:26656,91d50a7faf28fe301085f340a7d98a518e1243bd@44.236.220.165:26656"`
  
After you are done editing `config.toml` be sure to press CTRL+X and save any changes you made.  

You are now ready to [sync your node](https://github.com/reversesigh/cosmos_node-initial_setup/blob/main/05_sync.md) 
