## libinput

#### Force natural scrolling mode
  Add the following to /usr/share/X11/xorg.conf.d/50-synaptics.conf:
    `Section "InputClass"`
        `Identifier "libinput touchpad catchall"`
        `MatchDevicePath "/dev/input/event*"`
        `Driver "libinput"`
        `Option      "NaturalScrolling"          "true"`
    `EndSection`

#### Force natural scrolling mode (this method worked in Arch Linux):
  Add the following to /usr/share/X11/xorg.conf.d/40-libinput.conf in the touchpad catchall section:
  `Option "NaturalScrolling" "on"`

