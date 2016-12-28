## find

###### Better way to adjust permissions
  `$ find /path/to/something/ -type f -exec chmod 644 {} \;`
  `$ find /path/to/something/ -type d -exec chmod 755 {} \;`

###### The same, but possibly faster
  `$ find /path/to/something/ -type d -not -perm 755 -exec chmod 755 {} \;`
  `$ find /path/to/something/ -type f -not -perm 644 -exec chmod 644 {} \;`

###### Recursively delete all directories with specific name
  `$ find . -type d -name .mediaartlocal -exec rm -rf {} \;`

###### Remove files older than a specific number of days
  `$ find /path/containing/files/* -mtime +90 -exec rm {} \;`

###### Recursively delete all directories with specific name
  `$ find . -type d -name .mediaartlocal -exec rm -rf {} \;`

###### Recursively change spaces to underscores
  `$ find /dir -depth -name "* *" -execdir rename 's/ /_/g' "{}" \;`

###### Recursively remove hyphens and one underscore
  `$ find /home/jay/downloads/test -depth -name "*-_*" -execdir rename 's/_-//' "{}" \;`

###### Change file names of all files in current directory to lower case
  `$ find . -depth -exec rename 's/(.*)\/([^\/]*)/$1\/\L$2/' {} \;`

###### Find files less than a certain size
  `$ find . -type f -size -10 -ls`

###### Find files older than 6 days, and compress them individually
  `$ find . -type f -mtime +6 -exec gzip {} \;`

###### Remove a special character from all files recursively
  `$ find . -type f | rename "s/\'//g"`