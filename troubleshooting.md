# Troubleshooting common issues

## I've authored a Video-CD but my Philips CD-i is not detecting a disc

The Philips CD-i lacks an integrated movie player application for Video-CDs. It has to be supplied as part
of the medium to be an actual compliant Video-CD.

## I've authored a Video-CD but my Philips CD-i is making weird noises playing it. Actually it is not really playing the movies at all.

You might have used `FFmpeg` to mux. Please remux the stream using `mplex` or [TMPGEnc](tmpgenc.md) to fix this

## raw mode2 file must have size multiple of 2336

The CD-i bridge files you are trying to include, are broken. Please read about that [here](vcd.md)

## TMPGEnc refuses to open my source files

    File "xyz.avi" can not open, or unsupported.

This results from Wine not distributing working versions of Microsoft DirectShow.
[Please read here on how to fix this](tmpgenc.md)

## My encoded video has "pumping artefacts" or periodic quality issues

You might have used the MPEG1 encoder of [FFmpeg](ffmpeg.md) to encode the actual VCD compatible stream.
It is problematic when encoding I-Frames with lots of data. Please use [TMPGEnc](tmpgenc.md) instead for better results.
