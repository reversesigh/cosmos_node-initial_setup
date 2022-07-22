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
