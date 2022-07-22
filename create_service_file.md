# There are two ways I find easiest to create service files.  

## Method One  
Change `noded` to your binary name such as `gaiad`  
  
`sudo touch /etc/systemd/system/noded.service`  
`sudo nano /etc/systemd/system/noded.service`  
  
 Copy and paste the example.service file from this repo. Double the check to location of your node binary on the `ExecStart` line. Fill in as needed. An example:  
   
 `Description=Gaia daemon`  
`After=network-online.target`  

`[Service]`  
`User=gaia`  
`ExecStart=/home/gaia/go/bin/gaiad start`  
`Restart=on-failure`  
`RestartSec=3`  
`LimitNOFILE=4096`  
  
`[Install]`  
`WantedBy=multi-user.target`  
  
## Method Two
Create the file within CLI  
  
`cat <<EOF >> /etc/systemd/system/{daemon}.service`  
`[Unit]`  
`Description=Gaia daemon`
`After=network-online.target`  
  
`[Service]`  
`User=root`  
`ExecStart=/root/go/bin/gaiad start`  
`Restart=on-failure`  
`RestartSec=3`  
`LimitNOFILE=4096`  
  
`[Install]`  
`WantedBy=multi-user.target`  
`EOF`  
  
 # Enable the Service  
 Be sure to enable your service file so it starts when your server boots.  
   
 `sudo systemctl enable gaiad`  
 `sudo systemctl daemon-reload`  
   
 You can then start your service.  
 `sudo systemctl start gaiad`  
   
 Check the status by running the following  
 `sudo journalctl -u gaiad -f --output cat`  
