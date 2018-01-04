## SSH

###### Generate a secure key:
  `ssh-keygen -t ed25519 -a 100 -C jay`

###### Change ssh passphrase without changing the key:
  `$ ssh-keygen -f ~/.ssh/id_rsa -p`

###### Add your passphrase to the ssh-agent:
  `$ ssh-add ~/.ssh/id_rsa`
