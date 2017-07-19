## Xorg

###### Start an additional X session:
  In a new TTY, type: `startx -- :1`

##### Previous issues:
  According to the bug report (bug 1634449) occassional screen blackouts can be solved via (untested):
  sudo cp /usr/share/doc/xserver-xorg-video-intel/xorg.conf /etc/X11/
