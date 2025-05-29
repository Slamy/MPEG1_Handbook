# FFmpeg

FFmpeg is a popular and powerful tool for multimedia transcoding.
It is free, open source and usually part of every Linux distribution out there.

**Warning: The MPEG1 encoder of FFmpeg is broken at low constant bitrate usage and might produce low quality I-Frames**

## Encoding for Video-CDs

FFmpeg defines some presets for
encoding Video-CD MPEG1 streams.
According to the [documentation](https://ffmpeg.org/ffmpeg.html#Video-Options)
these are the resulting parameters when using those presets. This knowledge is helpful in case
one wishes to manipulate a few of them.

    pal:
    -f vcd -muxrate 1411200 -muxpreload 0.44 -packetsize 2324
    -s 352x288 -r 25
    -codec:v mpeg1video -g 15 -b:v 1150k -maxrate:v 1150k -minrate:v 1150k -bufsize:v 327680
    -ar 44100 -ac 2
    -codec:a mp2 -b:a 224k

    ntsc:
    -f vcd -muxrate 1411200 -muxpreload 0.44 -packetsize 2324
    -s 352x240 -r 30000/1001
    -codec:v mpeg1video -g 18 -b:v 1150k -maxrate:v 1150k -minrate:v 1150k -bufsize:v 327680
    -ar 44100 -ac 2
    -codec:a mp2 -b:a 224k

Here an example with the PAL preset while at the same time cropping the 16:9 footage to 4:3:

    ffmpeg -y -i "big_buck_bunny_1080p_h264.mov" -filter:v 'crop=ih/3*4:ih' -target pal-vcd bunny.mpg

The result might not be compatible with the VCD player on Philips CD-i. This can be fixed by properly remuxing it.

Here an example for demuxing the file into its elementary streams

    ffmpeg -y -i bunny.mpg -vcodec copy -an bunny.m1v
    ffmpeg -y -i bunny.mpg -acodec copy -vn bunny.mp2

These two streams can be muxed again for compatibility.
Use either `mplex` or `TMPGEnc` for this.

    mplex -f 1 bunny.mp2 bunny.m1v -o bunny_fixed.mpg

## Encoding for `pink` to allow inclusion in CD-i titles

The resolution doesn't need to comply to Video-CD standards. Apart from that, it is very similar to Video-CD.
`pink` requires the elementary streams.

    ffmpeg -y -i "big_buck_bunny_1080p_h264.mov" -r 25 \
        -vf "scale=384:256" -b:v 1150k -minrate 1150k -maxrate 1150k -bufsize 224k bunny.m1v
    ffmpeg -y -i "big_buck_bunny_1080p_h264.mov" -b:a 224k -ar 44100 bunny.mp2

## Preparing a high quality downscaled version for using TMPGEnc as the final encoder

Since FFmpeg suffers from bad I-Frame quality, here an example to prepare a high quality stream for encoding using
[TMPGEnc](tmpgenc.md) to aim for a higher quality final result.
At the same time, it crops 16:9 to 4:3 and scales it to a more fitting resolution.
This is for PAL.

    ffmpeg -y -i "big_buck_bunny_1080p_h264.mov" \
        -filter_complex '[0:v]crop=ih/3*4:ih[cropped];[cropped]scale=352x288[scaled]' \
        -r 25 -map "[scaled]" -q:v 0 bunny.avi

Don't forget, this only encodes video data. But you can use this to have the audio stream as separate file.

    ffmpeg -y -i "big_buck_bunny_1080p_h264.mov" -b:a 224k -ar 44100 bunny.mp2

