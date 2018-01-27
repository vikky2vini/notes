## sed

###### Remove a line from a file (when the line contains slashes)
  `sed '\|^/dev/xvdb|d' /etc/fstab`
  Note: When you use a non-standard delimeter, the delimeter needs to be escaped
