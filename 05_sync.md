## Start sync! :)  
  
There are different methods available for syncing your server.

1. Full Sync from the very first block - this will take a long time and requires upgrading chains along your sync journey.
2. Snapshot Sync - download a chain snapshot and extract to your data folder, start syncing from the latest block provided in snapshot.
3. State Sync - Sync the node starting from a defined trusted height and hash (fastest!)

## Snapshot Sync

Assuming you've downloaded your compressed snapshot already, you can extract using a command similar to the following example.

`lz4 -c -d snapshot.tar.lz4  | tar -x -C $HOME/.gaia`

This will extract the snapshot to your chain data folder. Once complete, you should be able to sync from that point.

`sudo systemctl start gaiad && sudo journalctl -u gaiad -f --output cat`  
  
## State Sync

This is my preferred method for syncing up a new node. Run a command similar to this one one most chains to get a trusted hash and block height. Replace `ipaddress` with a public RPC address:

`curl -s http://ipaddress:26657/commit | jq "{height: .result.signed_header.header.height, hash: .result.signed_header.commit.block_id.hash}"`

You can then enabled state sync in `config.toml` and input the information for state sync. Remember to include two entires for `rpc_servers`:  
  
`# For Cosmos SDK-based chains, trust_period should usually be about 2/3 of the unbonding time (~2`   
`# weeks) during which they can be financially punished (slashed) for misbehavior.`  
`rpc_servers = ""`  
`trust_height = 0`  
`trust_hash = ""`  
`trust_period = "168h0m0s"`  
  
You can also find working state sync settings via [Polkachu](https://polkachu.com/state_sync/cosmos) 

Once your state sync settings are set, run the following command.

`sudo systemctl start gaiad && sudo journalctl -u gaiad -f --output cat`  

You can check the status of your sync by running the following command.

On the server run `curl localhost:26657/status` (change port if needed)  
On a local machine run `curl nodeip:26657/status` (change port if needed) 

Once you see `"catching_up": false` then you know you are fully synced. Congratulations.
  
Now that youre node is fully synced and live, let's make an [SSH Key](https://github.com/reversesigh/cosmos_node-initial_setup/blob/main/06_ssh_key_login.md)  
