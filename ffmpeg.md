## ffmpeg

###### Cut portion from the beginning:
    `ffmpeg -ss 00:17:12 -i test.avi -codec copy cut.avi`

###### Cut portion from a specific point to the end:
    `ffmpeg -t 00:07:06 -i cut.avi -codec copy cut2.avi`
