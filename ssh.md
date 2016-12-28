## SSH

###### Change ssh passphrase without changing the key:
  `$ ssh-keygen -f ~/.ssh/id_rsa -p`

###### Add your passphrase to the ssh-agent:
  `$ ssh-add ~/.ssh/id_rsa`
