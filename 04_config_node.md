## app.toml

Direct yourself to your node's configuation folder.  
  
`cd ~/.gaiad/config/`  
  
Set your preferred pruning settings. Here is an example:  
`pruning="custom" && \`  
`pruning_keep_recent=107 && \`  
`pruning_keep_every=0 && \`  
`pruning_interval=73 && \`  
`sed -i -e "s/^pruning *=.*/pruning = \"$pruning\"/" app.toml && \`  
`sed -i -e "s/^pruning-keep-recent *=.*/pruning-keep-recent = \"$pruning_keep_recent\"/" app.toml && \`  
`sed -i -e "s/^pruning-keep-every *=.*/pruning-keep-every = \"$pruning_keep_every\"/" app.toml && \`  
`sed -i -e "s/^pruning-interval *=.*/pruning-interval = \"$pruning_interval\"/" app.toml`  
  
If you are using custom ports, please remember to edit LCD and gRPC as needed. Also be mindful of minimum gas fees, especially if you are a valiadtor. Refer to official docs for more information.    
  
`nano ~/.gaia/config/app.toml`  

CTRL+X and save any changes you made.
  
## config.toml  

Direct yourself to your node's configuation folder.  
  
`cd ~/.gaiad/config/`  

This is the main configuration file for your node. If you are using default ports there is not much that needs changed here. If you are using custom ports, be sure to edit them here and verify UFW settings before launching your node.

If you wish to access your node remotely from a local machine, you'll also need to expose the node's RPC by changing it's IP address to `0.0.0.0`
