# There are two ways I find easiest to create service files.  

## Method One  
Change `gaiad` to the name of the node you are installing.  
  
`sudo touch /etc/systemd/system/gaiad.service`  
`sudo nano /etc/systemd/system/gaiad.service`  
  
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
`ExecStart=/home/gaia/go/bin/gaiad start`  
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
