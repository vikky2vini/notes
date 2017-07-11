## irc

###### Register a nick and also set a password:
  `/msg nickserv register your_password your_email_address`

###### Change password:
  `/msg nickserv set password <NewPassword>`

###### Change nick:
  `/nick new_nick`

###### View information
  `/msg NickServ Info`

###### Change registration email
  `/msg NickServ set email myemail@domain.com`

###### Resend confirmation email
  `/query nickserv resend`

## irssi specific

###### Automatically connect to a server on startup
  `/server add -auto -network Freenode irc.freenode.net 6667`

###### Automatically identify on startup
  `/network add -autosendcmd "/msg nickserv identify password ;wait 2000" Freenode`

###### Automatically join a channel
  `/channel add -auto #ubuntu freenode
