## cmus

###### Compiling from source:
  1. Download cmus: https://cmus.github.io/#download
  2. Install dependencies (Ubuntu):
    ```# apt-get install libncursesw5-dev libpulse-dev libjack-dev libsamplerate-dev libopusfile-dev libavformat-dev libcue-dev libasound-dev libflac-dev libvorbis-dev libwavpack-dev libfaad-dev libmp4v2-dev libmad0-dev```
  3. Install dependencies (Fedora):
     ```# dnf install alsa-lib-devel ffmpeg-devel flac-devel jack-audio-connection-kit-devel libao-devel libcddb-devel libcdio-paranoia-devel libcue-devel libdiscid-devel libmad-devel libmodplug-devel libsamplerate-devel libvorbis-devel ncurses-devel opusfile-devel pulseaudio-libs-devel wavpack-devel```
  4. Make and install the package:
     ```./configure CONFIG_ROAR=n```

    ```make && sudo make install```

###### Previous issues
When cmus was complaining about the output device, the following fixed it:
    ```:set output_plugin=pulse```
