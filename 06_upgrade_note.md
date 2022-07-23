## A note on upgrades  
Later on when you need to run a chain upgrade, you can simply return to your cloned repo and run:  
  
`git fetch --tags`  
  
New tags will post, verify version tag with official announcements and then run:  
  
`git checkout vx.x.x`  
`sudo systemctl stop gaiad` (for safety, you may wish to backup your chain data folder at `~/.gaia/data/`)  
`make install`  
  
 Verify the new version  
   
 `gaiad version`  
 
 Restart the service and watch the log  
`sudo systemctl restart gaiad && sudo journalctl -u gaiad -f --output cat`  
  
Eventually, you may wish to learn about alternative methods such as [Cosmovisor](https://github.com/provenance-io/cosmovisor)  
  
## Important  
Sometimes chain upgrades will have specific instructions. *ALWAYS* refer to official announcements from chains for instructions.


Congratulations on setting up a full node! Check out some [addtional resources](https://github.com/reversesigh/cosmos_node-initial_setup/blob/main/07_resources.md) to help continue your journey.
