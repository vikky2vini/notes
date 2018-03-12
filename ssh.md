## SSH


###### Generate a 4096-bit RSA key:
  `ssh-keygen -t rsa -b 4096`

###### Generate a secure ed25519 key:
  `ssh-keygen -t ed25519 -a 100 -C jay`

###### Change ssh passphrase without changing the key:
  `$ ssh-keygen -f ~/.ssh/id_rsa -p`

###### Add your passphrase to the ssh-agent:
  `$ ssh-add ~/.ssh/id_rsa`
