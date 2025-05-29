# MEncoder

MEncoder belongs to the MPlayer project. The latter is popular media player on Linux.

**Warning: The MPEG1 encoder of mencoder is broken at low bitrates and might produce low quality I-Frames**

In a certain way, mencoder is similar in lack of quality as FFmpeg. Maybe they share the same encoder?

    mencoder -oac lavc -ovc lavc -of mpeg -mpegopts format=xvcd -vf \
        scale=352:288,harddup -srate 44100 -af lavcresample=44100 -lavcopts \
        vcodec=mpeg1video:keyint=15:vrc_buf_size=327:vrc_minrate=1152:vbitrate=1152:vrc_maxrate=1152:acodec=mp2:abitrate=224 \
        -ofps 25 -o bunny.mpg big_buck_bunny_1080p_h264.mov


**I advise not to use the result without thorough inspection!**
