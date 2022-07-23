Whenever you see `gaia` or `gaiad` used make sure to replace with whatever node you are installing.


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
  
It's time to edit `app.toml` directly. Please remember to edit LCD and gRPC as needed (edit ports, enable/disable RPC or API, etc.,). Also be mindful of minimum gas fees, especially if you are a valiadtor. Refer to official docs for more information. To get started open the `app.toml` file.   
  
`nano ~/.gaia/config/app.toml`  
  
CTRL+X and save any changes you made.  
  
  
## config.toml  

Direct yourself to your node's configuation folder.  
  
`cd ~/.gaiad/config/`  
`nano config.toml`  

This is the main configuration file for your node. If you are using default ports there is not much that needs changed here. If you are using custom ports, be sure to edit them here and verify UFW settings before launching your node.

If you wish to access your node remotely from a local machine, you'll also need to expose the node's RPC by changing the IP address to `0.0.0.0` in the RPC section  

You'll also need to add peers before you start syncing. Most blockchains will have a network repository featuring peer lists, genesis files, etc., Another great option is to use Polkachu if they have the chain resources available on their website. You can find resources for state sync, snapshot sync, peers, etc.,
  
An example of what Polkachu offers:  
[Polkachu - Cosmos Hub Resources](https://polkachu.com/networks/cosmos)  
  
After you are done editing `config.toml` be sure to press CTRL+X and save any changes you made.  
  
## Start sync! :)  
  
Once your configuration is complete and your state sync or snapshot sync is prepared, then you should be able to start your service and monitor the log live.    

`sudo systemctl start gaiad && sudo journalctl -u gaiad -f --output cat`  

You can check the status of your sync by running the following command.

On the server run `curl localhost:26657/status` (change port if needed)  
On a local machine run `curl nodeip:26657/status` (change port if needed) 

Once you see `"catching_up": false` then you know you are fully synced. Congratulations.
  
Now that youre node is fully synced and live, let's make an [SSH Key](https://github.com/reversesigh/cosmos_node-initial_setup/blob/main/05_ssh_key_login.md)  
