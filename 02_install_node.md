## Node Intallation  
One of the benefits of using Cosmos nodes is that the vast majority of them run and install exactly the same (there are exceptions that will not be compatible with this guide, such as `Secret Network` `Odin Protocol` or `Orai`). There are various ways users and admins can handle an installation. This guide assumes you find it easier to clone the repository and install manually. Other options include using Cosmovisor and other tools which are covered in other guides on the web.  
  
Whenever you see `gaia` or `gaiad` used make sure to replace with whatever node you are installing.  
  
## Clone the Repo and Checkout Correct Version  
For this guide we will be using `gaiad` as the example. This is assuming you have already setup your node initially following readme.md. For the majority of the time these same commands will work by simply replacing values such as URLs and names when installing other nodes.  
  
`git clone https://github.com/cosmos/gaia.git`  
`cd gaia`  
`git fetch --tags`  
`git checkout vx.x.x`  
  
## Install  
`make install`  

The binary will typically be installed in `/home/gaia/go/bin` (based on your environment settings and node user name).  
  
## Check Version  
`gaiad version`  

## Init your Node  
Confirm the current chain-id before running.  
  
`gaiad init moniker --chain-id cosmoshub-4`  

## Download Genesis  
Sometimes you'll be required to replace the current `genesis.json` file (localed in `/home/gaia/.gaiad/config/` with a newer one. Refer to chain docs or the chain's network repository.  
  
You are now ready to configure your node in `app.toml` and `config.toml`, which should be located in `/home/gaia/.gaia/config`.
  
## A note on upgrades  
Later on when you need to run a chain upgrade, you can simply return to this folder and run:  
  
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
