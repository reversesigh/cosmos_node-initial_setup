Instead of typing out `ssh -p xxxx username@ipaddress` to login to your node's server, you can create an ssh key and configure your local machine to access with a simple command such as `ssh gaianode`.  
  
On your local machine, run the following (for Windows or Mac users, please refer to other guides):  
  
`ssh-keygen -f ~/.ssh/keyname -t rsa -b 4096`  

Your options for `-t` include `rsa` `dsa` `ecdsa` or `ed25519`. Refer to `ssh-keygen` guides online for more information on type and size.  

## Create .ssh/config Entry  
  
`nano .ssh/config`  
  
Add the following:  
`# ServerName`  
`Host gaianode`  
` HostName ipaddress`  
 `Port xxxx`  
 `User username`  
 `IdentityFile ~/.ssh/keyname`  
   
CTRL+X and save your file. Run the following command:  
  
`ssh-copy-id -i .ssh/keyname gaianode`  

You'll be prompted for your server password. The public key should upload to your server. You'll now simply type the following to login to your server without the need of typing a password:  
  
`ssh gaianode`  

Make sure to edit `gaianode` to match your own needs/settings.
