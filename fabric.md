## Fabric

###### To view the help menu:
  `$ fab -h`

###### To list all your fabric functions:
  `$ fab -l`

###### To specify the user name to use with remote hosts:
  `env.user = 'username'`

###### To specify remote machines to connect to:
  `env.hosts = ['myserver']`
  `env.hosts = ['myserver:65010']`

###### To run the commands asynchronously:
  `fab -P`

###### To call fabric with arguments:
  `fab scan_subnet:254`


###### Functions:
	get(remote_path, local_path=None)
Allows you to pull files from the remote machine to your local machine.

    local(command, capture=False)
Allows you to take action on the local host in a similar fashion to the Python subprocess module (in fact, local is a simplistic wrapper that sits on top of the subprocess module). Simply supply the command to run and, if needed, 	whether you want to capture the output. If you specify capture=True, the output will be returned as a string from local, otherwise it will be output to STDOUT.

    open_shell(command=None)
Mostly for debugging purposes. It opens an interactive shell on the remote end, allowing you to run any number of commands.

    prompt(text, key=None, default='', validate=None)
When you need to supply a value, but don't want to specify it on the command line for whatever reason, prompt is the ideal way to do this.

    put(local_path, remote_path, use_sudo=False, mirror_local_mode=False, mode=None)
This is the opposite command of get, although you are given more options when putting to a remote system than getting. The local path can be a relative or absolute file path, or it can be an actual file object. If either local_path or remote_path is left blank, the working directory will be used. If use_sudo=True is specified, Fabric will put the file in a temporary location on the remote machine, then use sudo to move it from the temporary location to the specified location. This is particularly handy when moving system files like /etc/resolv.conf or the like that can't be moved by a standard user and you have root login turned off in SSH. If you want the file mode preserved through the copy, use mirror_local_mode=True; otherwise, you can set the mode using mode.

    reboot(wait=120)
Reboots the remote machine. By default, reboot will wait 120 seconds before attempting to reconnect to the machine to continue executing any following commands.

    require(*keys, **kwargs)
Forces the specified keys to be present in the shared environment dict in order to continue execution. If these keys are not present, Fabric will abort. Optionally, you can specify used_for to indicate what the key is used for in this particular context.

    run(command, shell=True, pty=True, combine_stderr=True, quiet=False, warn_only=False, stdout=None, stderr=None)
Executes commands on the remote host. With run, you execute the specified command as the given user. run returns the output from the command as a string that can be checked for a failed, succeeded and return_code attribute. shell controls whether a shell interpreter is created for the command. If turned off, characters will not be escaped automatically in the command. Passing pty=False causes a psuedo-terminal not to be created while executing this command; this can have some benefit if the command you are running has issues interacting with the psuedo-terminal, but otherwise, it will be created by default. If you want stderr from the command to be parsable separately from stdout, use combine_stderr=False to indicate that. quiet=True will cause the command to run silently, sending no output to the screen while executing. When an error occurs in Fabric, typically the script will abort and indicate as such. You can indicate that Fabric need not abort if a particular command errors using the warn_only argument. Finally, you can redirect where the remote stderr and stdout redirect to on the local side. For instance, if you want the stderr to pipe to stdout on the local end, you could indicate that with stderr=sys.stdout.

    sudo(command, shell=True, pty=True, combine_stderr=True, user=None, quiet=False, warn_only=False, stdout=None, stderr=None, group=None)
sudo works precisely like run, except that it will elevate privileges prior to executing the command. It basically works the same is if you'd run the command using run, but prepended sudo to the front of command. sudo also takes user and group arguments, allowing you to specify which user or group to run the command as. As long as the original user has the permissions to escalate for that particular user/group and command, you are good to go.

#### Useful articles:
[Fabric tutorial](http://awaseroot.wordpress.com/2012/04/23/fabric-tutorial-1-take-command-of-your-network/)

[How to use Fabric in Python](http://www.pythonforbeginners.com/systems-programming/how-to-use-fabric-in-python/)

[Fabric - System Administratiors best friend](http://www.linuxjournal.com/content/fabric-system-administrators-best-friend)