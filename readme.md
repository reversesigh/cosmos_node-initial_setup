# Iniital Setup Guide for Cosmos Nodes
Written form the perspective of using Ubuntu with a dedicated server, but most of this will apply if you are running a physical machine as well.

## LOGIN
`ssh root@ipaddress`

## Update & Upgrade Repos
`apt update && apt upgrade -y`

## Add Users
`adduser username`  
`adduser nodename`  

## Give User Sudo
`usermod username -aG sudo`  
`usermod nodename -aG sudo`

## Switch to Node user
`su - nodename`

## Install Standard Dependencies
`sudo apt install make build-essential gcc git jq chrony -y`

## Install go, check https://go.dev/dl for latest version before running
`wget https://golang.org/dl/go1.18.4.linux-amd64.tar.gz`  
`sudo tar -C /usr/local -xzf go1.18.4.linux-amd64.tar.gz`

## Setup go in .profile
`cat <<EOF >> ~/.profile`  
`# Go`  
`GOROOT=/usr/local/go`  
`GOPATH=$HOME/go`  
`GO111MODULE=on`  
`PATH=$PATH:/usr/local/go/bin:$HOME/go/bin`  
`EOF`

## Reset shell session
`source ~/.profile`

## Look for go
`go version`  
`which go`

## SSH Configuration
`sudo nano /etc/ssh/sshd_config`

## Uncomment 'Port 22' and change '22' to 'xxxx' (xxxx = custom port #)

Uncomment `Port 22` and change `22` to `xxxx` (xxx = custom port)  
Add `ActiveUsers username1 username2` to restrict ssh login to defined users only

CTRL+X and save your file  
`sudo systemctl restart sshd`

## UFW Rules (these are default ports, please set rules according to your setup)
`sudo ufw default allow outgoing`  
`sudo ufw default deny incoming`  
`sudo ufw allow xxxx`  
`sudo ufw allow 26656`  
`sudo ufw allow 9090`

## Open RPC (default: 26657) to your specific machine's IP address to connect to your node to use cli client from local machine
`sudo ufw allow from youripaddress to any port 26657`  
`sudo ufw enable`

## Confirm with UFW that port xxxx is open for ssh
`sudo ufw status`

## Open as second terminal session and try to login using your user's creditinals.
`ssh -p xxxx user@ipaddress`

## Test sudo and root access
`sudo -i`  
`exit`

## Restrict Root Login
`sudo nano /etc/ssh/sshd_config`
 
## Change 'PermitRootLogin' from "Yes" to "No" and confirm it is uncommented then: 
`CTRL+X and Save`  
`sudo systemctl restart sshd`

## Exit Root & User
`exit`

## Verify Root Login is Disabled
`ssh -p xxxx root@ipaddress`

## After this, node is ready for setup. Each node should have an up to date guide on their GitHub or Docs pages to get started.

Some examples  
BitCanna https://docs.bitcanna.io/guides/validator-setup-guide  
Chihuahua https://github.com/ChihuahuaChain/mainnet  
Cosmos https://github.com/cosmos/gaia/blob/main/docs/hub-tutorials/join-mainnet.md  
Osmosis https://github.com/osmosis-labs/osmosis  
Secret https://github.com/scrtlabs/SecretNetwork/blob/master/docs/validators-and-full-nodes/run-full-node-mainnet.md
