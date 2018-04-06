## SSH

#### Key management
###### Generate a 4096-bit RSA key:
  `ssh-keygen -t rsa -b 4096`

###### Generate a secure ed25519 key:
  `ssh-keygen -t ed25519 -a 100 -C jay`

###### Change ssh passphrase without changing the key:
  `$ ssh-keygen -f ~/.ssh/id_rsa -p`

###### Add your passphrase to the ssh-agent:
  `$ ssh-add ~/.ssh/id_rsa`

#### Tunneling
###### Create a SOCKS proxy to tunnel your web traffic
  `ssh -D <port> <remote_host>`
  Set your web browser to use `localhost:<port>` as the proxy.

###### Connect to a Windows RDP host behind a bastion server
  `ssh -L <port>:<target_host>:3389 <bastion_server>`
  Set your RDP client to connect to `localhost:<port>`

###### Connect to your remote machine’s VNC server without opening the VNC port
  `ssh -L 5901:localhost:5901 <remote_host>`
  `Set your VNC client to to connect to localhost:5901`
