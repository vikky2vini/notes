## pacman

###### Check for orphans
  `$ pacman -Qdt`

###### Remove orphans
  `# pacman -Rs $(pacman -Qqdt)

###### Find out which package owns a file:
  `$ pacman -Qo /path/to/file

###### Find out what provides a dependency:
  `$ pacman -Fs libldns.so.1`

###### Ignore a group of packages:
  IgnoreGroup = x
