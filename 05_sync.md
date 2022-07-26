## Start sync! :)  
  
There are different methods available for syncing your server.

1. Full Sync from the very first block - this will take a long time and requires upgrading chains along your sync journey.
2. Snapshot Sync - download a chain snapshot and extract to your data folder, start syncing from the latest block provided in snapshot.
3. State Sync - Sync the node starting from a defined trusted height and hash (fastest!)

## Snapshot Sync

Assuming you've downloaded your compressed snapshot already, you can extract using a command similar to the following example. If you need to download a snapshot check with [Polkachu](https://polkachu.com/), [Stake2Me](https://snapshots.stake2.me/), [Quicksync](https://www.quicksync.io/), [Stakecraft](https://snapshots.stakecraft.com/), among many others.
  
Extract your snapshot to your data folder. This command may change depending on the file type of the archive:  
  
`lz4 -c -d snapshot.tar.lz4  | tar -x -C $HOME/.gaia`

This will extract the snapshot to your chain data folder. Once complete, you should be able to sync from that point.

`sudo systemctl start gaiad && sudo journalctl -u gaiad -f --output cat`  
  
## State Sync

This is my preferred method for syncing up a new node. Run a command similar to this one one most chains to get a trusted hash and block height. Replace `Polkachu`'s RPC in the example with a public RPC address that fits your needs (for example if you are trying to state sync Comdex, you'll need to find a Comdex RPC instead):  
  
`curl -s https://cosmos-rpc.polkachu.com:443/commit | jq "{height: .result.signed_header.header.height, hash: .result.signed_header.commit.block_id.hash}"`

You can then enable state sync in `config.toml` and input the information for state sync. Remember to include two entires for `rpc_servers`:  
  
Default setting:  
  
`rpc_servers = ""`  
`trust_height = 0`  
`trust_hash = ""`  
`trust_period = "168h0m0s"`  
  
Here is an example of what your edited configuration for state sync should look like: 
  
`rpc_servers = "https://cosmos-rpc.polkachu.com:443,https://cosmos-rpc.polkachu.com:443"`  
`trust_height = 11377513`  
`trust_hash = "E95A010386958C240862CD934D6B46D8104EEDECCCF3249613E31B13E9E22CC1"`  
`trust_period = "168h0m0s"`  

Make sure State Sync is enabled as well.  
  
`[statesync]`  
`enable = true`  
  
You can also find working state sync settings via [Polkachu](https://polkachu.com/state_sync/cosmos). They provide a script you can execute that will automatically update your `config.toml` with the correct state sync settings.  

Once your state sync settings are set, run the following command.

`sudo systemctl start gaiad && sudo journalctl -u gaiad -f --output cat`  

## Sync Status

You can check the status of your sync by running the following command.

On the server run `curl localhost:26657/status` (change port if needed)  
On a local machine run `curl nodeip:26657/status` (change port if needed) 

Once you see `"catching_up": false` then you know you are fully synced. Congratulations.
  
Now that youre node is fully synced and live, let's make an [SSH Key](https://github.com/reversesigh/cosmos_node-initial_setup/blob/main/06_ssh_key_login.md)  

## A note on unsafe-reset-all  
  
You may notice that the command `unsafe-reset-all` in certain guides. Be *very* careful with this command, especially if you are a validator. There is a reason the word `unsafe` is used.  
  
Running this command will reset your chain data and reset your `priv_validator_state.json`to the genesis state. If you are a validator, always make sure you have your `priv_validator_key.json` backed up safely.  
  
An example of when you might want to use this is when your chain data becomes corrupted, requiring you to resync your node. You can run this command before extracting your snapshot or starting state sync: 
  
`gaiad tendermint unsafe-reset-all --home /home/gaia/.gaia/`  
  
I like to define `--home` in this command in case I'm in the wrong folder. You may notice if you run this command without the `--home` flag that it will create a `config` and `data` folder in your current directory instead of your default home folder for `gaia`. 
  
Other chains may include `unsafe-reset-all` as a main subcommand rather than a subcommand of `tendermint`. An example using another chain:  
  
`comdex unsafe-reset-all --home /home/comdex/.comdex/`  
