## svn

###### To list the contents of a repository or folder:
	svn list http://URL/svn/myproject

###### To create a new directory in the SVN repository:
	svn mkdir http://URL/svn/myproject/newdirname

###### To check out an SVN repository:
	svn co (or checkout) http://URL/svn/myproject PATH

###### To add a new file to an SVN repository:
	svn add local_path_to_new_file

###### To remove a file from an SVN repository:
	svn delete http://URL

###### To check in an SVN repository:
	svn ci (or commit) PATH

###### Show difference between your working copy and the SVN copy:
	svn diff filename

###### To view the SVN log:
	svn log http://URL (add a folder or file name if you want)

###### Setting up subversion on a server:
	1. Apache should be installed and configured
	2. Install subversion libapache2-svn apache2-utils
	3. Create a folder where svn files should be stored (/usr/local/svn or somewhere else)
	4. Create the 'subversion' user group: sudo groupadd subversion
	5. Add your user and the www-data user to the subversion group: usermod -aG subversion jlacroix
	6. touch /etc/subversion/passwd
	7. Add the first user: sudo htpasswd -c /etc/subversion/passwd jlacroix

[svn examples article](	http://www.thegeekstuff.com/2011/04/svn-command-examples/)
