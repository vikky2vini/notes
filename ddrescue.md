## ddrescue

#### Cloning a failed drive failed drive
###### Clone the failed drive to another drive, skipping bad sectors:
  `# ddrescue -f --no-split /dev/sdb /dev/sdc logfile`

###### Clone the failed drive to another drive, retrying bad sectors three times:
  `# ddrescue -f -r3 /dev/sdb /dev/sdc logfile`
