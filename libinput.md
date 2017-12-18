## libinput

#### Force natural scrolling mode
  Add the following to /usr/share/X11/xorg.conf.d/50-synaptics.conf:
    `Section "InputClass"`
        `Identifier "libinput touchpad catchall"`
        `MatchDevicePath "/dev/input/event*"`
        `Driver "libinput"`
        `Option      "NaturalScrolling"          "true"`
    `EndSection`
